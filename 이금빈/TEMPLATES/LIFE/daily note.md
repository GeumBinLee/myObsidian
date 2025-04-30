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
const currentDate = moment(title, 'YYYY-MM-DD');

const isoWeekTitle = currentDate.format("GGGG-[W]WW");
const monthlyTitle = currentDate.format("YYYY-MM");
const dayOfWeek = currentDate.format("ddd");

// 파일 이동: LIFE/YYYY/DAILY NOTE/MM/yyyy-mm-dd
const destinationFolder = `LIFE/${currentDate.format("YYYY")}/DAILY NOTE/${currentDate.format("MM")}`;
await tp.file.move(`${destinationFolder}/${title}`);
%>
> [!Note] 🏃🏻‍♀️Go to page🏃🏻‍♀️
> WEEKLY NOTE ➔ [[<% isoWeekTitle %>]]
> MONTHLY NOTE ➔ [[<% monthlyTitle %>]]

<% tp.web.daily_quote() %>

# MEMO
- [n] 그냥 메모
- [*] 중요 메모
- [?] 질문
- [i] 정보성 메모
- [I] 아이디어
- [S] 재무 관련
- [b] 북마크
- [\"] 인용

# GRATITUDE JOURNAL
1. 

# REVIEW
- [p] Good
- [c] Bad

# JOURNAL
> [!Quote] 오늘 일기 한줄로 요약하기 (아래 일기 작성)
> 
