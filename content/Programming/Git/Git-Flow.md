
> 안정적인 운영이 필요하면 Git Flow

게임개발과 같이 안정적인 Release를 해야 하는 분야에서 Git-Flow 전략을 많이 사용한다.

![[Pasted image 20231001233933.png]]
Git Flow 전략에서는 크게 5개 브랜치를 운영하는데

1. main 브랜치(배포용)
2. develop 브랜치(개발용)
3. feature 브랜치(develop에 기능 추가용)
4. hotfix 브랜치(main 브랜치 버그 해결용)
5. release 브랜치(develop 브랜치를 main 브랜치에 합치기 전에 최종 테스트용)

이렇게 5가지를 운영한다.

#### Git-Flow의 진행 과정
1. Develop 브랜치부터 생성
![[Pasted image 20231001233942.png]]
2. 신기능 개발은 feature 브랜치에서 진행
![[Pasted image 20231001234017.png]]
- feature 브랜치 작명할 때는 feature/guild, feature/friend 와 같은 식으로 작명함

3. 신버전 출시 준비는 release 브랜치
![[Pasted image 20231001234213.png]]
- release 브랜치에서는 테스트나 QA 같은걸 진행
- 완성된 것 같으면 main 브랜치로 merge 해 배포

4. hotfix 브랜치
![[Pasted image 20231001234301.png]]
- main 브랜치에서 긴급한 버그가 생기면 hotfix 브랜치를 생성해서 바로바로 버그 수정
- 수정이 완료되면 main, develop 양쪽 브랜치에 모두 merge

