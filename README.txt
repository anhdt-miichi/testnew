# Repo A: .github/workflows/trigger.yml
name: Trigger and Wait

on:
  workflow_dispatch:

jobs:
  trigger-and-wait:
    runs-on: ubuntu-latest
    steps:
      - name: Trigger repository_dispatch in Repo B
        run: |
          curl -X POST https://api.github.com/repos/<owner>/<repo-b>/dispatches \
            -H "Authorization: token ${{ secrets.GH_PAT }}" \
            -H "Accept: application/vnd.github.v3+json" \
            -d '{"event_type":"custom-trigger"}'

      - name: Wait for Repo B workflow to complete
        run: |
          echo "Waiting for Repo B workflow to start..."
          sleep 10
          MAX_RETRIES=30
          COUNT=0

          while [[ $COUNT -lt $MAX_RETRIES ]]; do
            RUN_ID=$(curl -s -H "Authorization: token ${{ secrets.GH_PAT }}" \
              https://api.github.com/repos/<owner>/<repo-b>/actions/runs \
              | jq '.workflow_runs[] | select(.event == "repository_dispatch") | .id' | head -n 1)

            if [[ -z "$RUN_ID" ]]; then
              echo "Workflow not found yet. Retrying..."
              sleep 10
              COUNT=$((COUNT+1))
              continue
            fi

            STATUS=$(curl -s -H "Authorization: token ${{ secrets.GH_PAT }}" \
              https://api.github.com/repos/<owner>/<repo-b>/actions/runs/$RUN_ID \
              | jq -r '.status')

            CONCLUSION=$(curl -s -H "Authorization: token ${{ secrets.GH_PAT }}" \
              https://api.github.com/repos/<owner>/<repo-b>/actions/runs/$RUN_ID \
              | jq -r '.conclusion')

            echo "Status: $STATUS, Conclusion: $CONCLUSION"

            if [[ "$STATUS" == "completed" ]]; then
              if [[ "$CONCLUSION" == "success" ]]; then
                echo "Workflow succeeded"
                exit 0
              else
                echo "Workflow failed"
                exit 1
              fi
            fi

            sleep 10
            COUNT=$((COUNT+1))
          done

          echo "Timed out waiting for workflow"
          exit 1

