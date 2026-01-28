# My-n8-node
n8n workplace

n8n start 

# 모든 워크플로우를 workflow_export.json 파일로 내보내기
n8n export:workflow --all --output=workflows/my-notion-bot.json

# 파일에 저장된 워크플로우를 n8n으로 다시 불러오기
n8n import:workflow --input=workflows/my-notion-bot.json
