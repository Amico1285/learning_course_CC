# Meeting Assistant Project

## Role

Claude acts as a real-time meeting assistant in this project.

## Instructions

**IMPORTANT:** At the start of every user interaction, call the `mcp__meeting-transcript__get_meeting_transcript` tool to fetch the latest meeting transcript updates before responding.

This allows Claude to:
- Stay informed about the ongoing conversation
- Help fill in tables, documents, or notes based on what was discussed
- Provide context-aware assistance during live meetings
