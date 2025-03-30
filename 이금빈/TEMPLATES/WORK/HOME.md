<%*
let title = tp.file.title || tp.file.path.split("/").pop().replace(".md", "");

const userTitle = await tp.system.prompt("이동할 폴더명을 입력하세요");

if (!userTitle) {
    console.warn("폴더명이 입력되지 않았습니다.");
} else {
    const destinationFolder = `🗂️ Project 🗂️/${userTitle}`;

    try {
        const folderExists = await app.vault.adapter.exists(destinationFolder);
        if (!folderExists) {
            await app.vault.createFolder(destinationFolder);
        }

        // 파일명을 사용자가 입력한 폴더명으로 변경
        await tp.file.rename(userTitle);

        // 파일을 이동 (파일명이 변경된 이후에 이동해야 함)
        await tp.file.move(`${destinationFolder}/${userTitle}`);
        
    } catch (error) {
        console.error("폴더 생성 또는 파일 이동 중 오류 발생:", error);
    }
}
%>


# 참고자료
> [!Note]- env 파일 내용
> ```bash
> FLAVOR=dev
> BASE_URL=
> DEEP_LINK_URL=
> KAKAO_NATIVE_APP_KEY=
> JAVA_SCRIPT_APP_KEY=
> ```
## 링크
- [🔗 링크1 🔗]()
## 테스트 플라이트
- 계정: ID / PW
- [[Test Flight 관련 자료]]

# TO DO LIST
## For Today
```tasks
filter by function ["TODO", "IN_PROGRESS"].includes(task.status.type) && !["Rescheduled", "Scheduled", "Location", "Cake", "Important"].includes(task.status.name)
due on today
tags include #<% title %>
```
## Back Log (with no tag)
- [ ] 

# MEMO
- [n] 