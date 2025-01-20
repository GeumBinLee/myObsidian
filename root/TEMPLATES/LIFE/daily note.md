---
title: daily note
created: 2025-01-20 @ 15:38
updated: 2025-01-20 @ 15:38
tags:
  - dailynote
mood: 
score:
---
<%*
const title = tp.file.title;
const today = moment().format("YYYY-MM-DD (ddd)");
const yesterday = moment(title).subtract(1, 'days').format("YYYY-MM-DD (ddd)");
const tomorrow = moment(title).add(1, 'days').format("YYYY-MM-DD (ddd)");
%>
⬅️  [[<% yesterday %>]] | [[<% tomorrow %>]]  ➡️
# <% title %>
<% tp.web.daily_quote() %>

## IMPORTANT SCHEDULE
- [<] 일정 1 (@<% today %>)
- [<] 일정 2 (@<% today %>)

## TO DO LIST
- [ ] 00:00 할 일 1 (@<% today %>)
- [ ] 00:00 할 일 2 (@<% today %>)

## MEMO
- 

## GRATITUDE JOURNAL
1. 