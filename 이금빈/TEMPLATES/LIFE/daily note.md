---
created: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
updated: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
tags:
  - dailynote
weather: 
moods: 
score:
---
<%*
const title = tp.file.title;
const today = moment(title).format("YYYY-MM-DD");
const yesterday = moment(title).subtract(1, 'days').format("YYYY-MM-DD");
const tomorrow = moment(title).add(1, 'days').format("YYYY-MM-DD");

// 현재 날짜의 연도와 월 계산
let weekYear = moment(title).year(); // 기본 연도
let month = moment(title).month() + 1;
let paddedMonth = String(month).padStart(2, "0");

// 해당 날짜의 월요일 찾기
const currentDate = moment(title);
const currentWeekMonday = currentDate.clone().startOf('isoWeek'); // 해당 날짜의 월요일
const monthStart = currentDate.clone().startOf('month'); // 이번 달 1일
let firstMonday = monthStart.clone();

// 이번 달 첫 번째 월요일 찾기
while (firstMonday.isoWeekday() !== 1) {
firstMonday.add(1, 'day');
}

// 이번 주의 월요일이 몇 번째 월요일인지 계산
let weekIndexInMonth = Math.floor(currentWeekMonday.diff(firstMonday, 'days') / 7) + 1;

// 이전 월 처리 (첫 월요일보다 앞선 날짜는 이전 월의 마지막 주차로 계산)
if (currentDate.isBefore(firstMonday)) {
const previousMonth = currentDate.clone().subtract(1, 'month').startOf('month');
let lastMonthMonday = previousMonth.clone();
while (lastMonthMonday.isoWeekday() !== 1) {
lastMonthMonday.add(1, 'day');
}
const lastMondayOfPreviousMonth = lastMonthMonday.clone();
while (lastMondayOfPreviousMonth.clone().add(7, 'days').isBefore(firstMonday)) {
lastMondayOfPreviousMonth.add(7, 'days');
}

// 이전 월 정보 반영
weekIndexInMonth = Math.floor(currentWeekMonday.diff(lastMonthMonday, 'days') / 7) + 1;
paddedMonth = String(previousMonth.month() + 1).padStart(2, "0");
weekYear = previousMonth.year();
}

// 위클리 노트 제목 설정 (월 기준 주차 적용)
const weeklyTitle = `${weekYear}-${paddedMonth}-W${String(weekIndexInMonth).padStart(2, "0")}`;
const dayOfWeek = moment(title).format("ddd"); // 요일만 출력 (예: Mon, Tue)

// 파일 이동
const destinationFolder = `LIFE/${weekYear}/DAILY NOTE/${paddedMonth}`; // 이동할 폴더 경로
await tp.file.move(`${destinationFolder}/${title}`);
%>
> [!Note] 🏃🏻‍♀️Go to page🏃🏻‍♀️
> YESTERDAY ➡️ [[<% yesterday %>]]
> TOMORROW ➡️ [[<% tomorrow %>]]
> WEEKLY NOTE ➡️ [[<% weeklyTitle %>]]
> MONTHLY NOTE ➡️ [[<% weekYear %>-<% paddedMonth %>]]

# <% title %> (<% dayOfWeek %>)
<% tp.web.daily_quote() %>
## HAVING A MEAL
- ⛅️ 아침 ⛅️: 
- ☀️ 점심 ☀️: 
- 🌕 저녁 🌕: 

## SCHEDULE
```tasks
path does not include LIFE/2025/DAILY NOTE/<% paddedMonth %>/<% title %>
scheduled on <% today %>
```

## TO DO LIST
### Postponed task for today
```tasks
path does not include LIFE/2025/DAILY NOTE/<% paddedMonth %>/<% title %>
due on <% today %>
created before <% today %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
### Today's tasks
```tasks
path does not include LIFE/2025/DAILY NOTE/03/<% today %>
# due on <% today %> # 원래 쿼리
happens on <% today %>
created on or after <% today %>
filter by function ["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type) && !['Scheduled', 'Rescheduled', 'Important', 'Location', 'Cake'].includes(task.status.name)
```
- [ ] 근력 운동 - [🔗 캐시 뒷벅지](https://www.youtube.com/watch?v=NnNl07xlPdU) __set + [🔗 소미핏 복근](https://youtu.be/p623pewgTc0) __set + [🔗 하체토닝 스쿼트 부분](https://youtu.be/ieGVQp_eRFs) __set + [🔗 심으뜸 서서 복근](https://youtu.be/kETh8T3it4k) __set ➕ <% today %> 📅 <% today %>
- [ ] 스트레칭 - [🔗 소미핏 골반](https://www.youtube.com/watch?v=fuaR_oV0nZc) + [🔗 강하나 하체](https://www.youtube.com/watch?v=fuaR_oV0nZc) + [🔗 이지은 종아리](https://www.youtube.com/watch?v=fuaR_oV0nZc) + [이지은 침대 종아리](https://youtu.be/doiSCQsxV58?feature=shared) ➕ <% today %> 📅 <% today %>
- [ ] #일본어 (Anki) 日本語 勉強 ➕ <% today %> 📅 <% today %>
- [ ] #영어 (Anki) Studying English ➕ <% today %> 📅 <% today %>
- [ ] 독서 - 「책 제목」 ➕ <% today %> 📅 <% today %>

## MEMO
```tasks
path includes LIFE/2025/WEEKLY NOTE/<% weeklyTitle %>
heading includes "<% today %> for <% dayOfWeek %>"
filter by function !["TODO", "IN_PROGRESS", "DONE", "CANCELLED"].includes(task.status.type)
```
- [n] 처리 순서:🕛새벽()🕛 → 🛏️오전()🛏️ → 🛌낮잠🛌 → ☀️오후()☀️ → 🌖밤()🌖
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
- [p] Good
- [c] Bad

## JOURNAL
> [!Quote] 오늘의 일기 한줄로 설명하기 (아래 일기 작성)
> 