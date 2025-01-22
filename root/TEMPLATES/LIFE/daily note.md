---
title: daily note
created: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
updated: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
tags:
  - dailynote
mood: 
score:
---
****<%*
const title = tp.file.title;
const today = moment(title).format("YYYY-MM-DD");
const yesterday = moment(title).subtract(1, 'days').format("YYYY-MM-DD (ddd)");
const tomorrow = moment(title).add(1, 'days').format("YYYY-MM-DD (ddd)");
const weekNumber = moment(title).isoWeek(); // ISO 주차 계산
const weekYear = moment(title).isoWeekYear(); // 해당 주차의 연도
const month = `${moment(title).month() + 1}월`;
const weeklyTitle = `${weekYear}년 ${month} ${weekNumber}주차`; // 위클리 제목 형식
%>
> [!tip] ==Go to page==
YESTERDAY ➡️ [[<% yesterday %>]]
TOMORROW ➡️ [[<% tomorrow %>]]
WEEKLY NOTE ➡️ [[<% weeklyTitle %>]]

# <% title %>
<% tp.web.daily_quote() %>

## SCHEDULE
```tasks
path includes LIFE/2025/WEEKLY NOTE
heading includes <% today %>
filter by function ['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
- [<] 일정 ⏳ <% today %> ➕ <% today %>
- [>] 미뤄진 일정⏳ <% today %> ➕ <% today %>
- [!] 중요한 일정⏳ <% today %> ➕ <% today %>
- [l] 오프라인 약속⏳ <% today %> ➕ <% today %>
- [w] 기념일⏳ <% today %> ➕ <% today %>
### Rescheduled for today
```tasks
scheduled on <% today %>
created before <% today %>
filter by function ['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```


## TO DO LIST
```tasks
path includes LIFE/2025/WEEKLY NOTE
heading includes <% today %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
- [ ] 1일 1커밋 📅 <% today %> ➕ <% today %>
- [ ] (Anki) 日本語 勉強 📅 <% today %> ➕ <% today %>
- [ ] (Anki) Studying English 📅 <% today %> ➕ <% today %>
- [/] IN PROGRESS 📅 <% today %> ➕ <% today %>
### Postponed task for today
```tasks
due on <% today %>
created before <% today %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```


## MEMO
```tasks
path includes LIFE/2025/WEEKLY NOTE
heading includes <% today %>
filter by function !["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type)
```
- [n] 노트 테이킹
- [*] 중요 메모
- [?] 질문
- [i] 정보성 메모
- [I] 아이디어
- [S] 재무 관련
- [b] 북마크
- ["] 인용

## GRATITUDE JOURNAL
1. 

## REVIEW
- [p] Good 1
- [p] Good 2
- [p] Good 3
- [c] Bad 1
- [c] Bad 2
- [c] Bad 3

## JOURNAL
> [!Quote] 오늘의 일기 한줄로 설명하기 (아래 일기 작성)
> 