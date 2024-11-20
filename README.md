#Github 

        * github 등록
            1. 저장소 생성 (github 사이트)
            2. git remote add origin 0000(주소)
            이미 등록 되 있으면 git remote remove origin 
            3. git push -u origin main

            # pull할 것이 있을때 psuh 하려면?
                git pull --rebase(협업시 주로사용) -> git push
                git pull --no-rebase(merge방식) -> git push

        * 기본설정 
            1. 터미널에 pwd를 입력해 현재 위치를 파악한다
            2. 현재위치가 원하는 파일이 아니라면 cd 000(파일명)을 통해 파일로 이동한다
            3. git init 으로 파일을 .git 파일로 만든다
            4. git config user.name "--"
            5. git config user.email "--"
            
        * 커밋 순서
            1. git add .
            2. git commit -m "--"
            or
            1. git commit -am "--" (이미 추적이 되있는 파일을 새롭게 추가하고 커밋 할 경우)
            
#####명령어(터미널)

        * pwd : 현재위치 파악
        * cd 000 : 위치 이동 
        * mkdir 0000 : 폴더생성
        
####명령어(git)

        * git remote -v : 주소확인
        * git config : 설정값 
        * git config global : 컴퓨터 파일 전체에 설정값 설정
        * git add 00 : 파일을 추적 해줌
        * git add . : 모든 파일을 추적
        * git re --cached.00 : 추적에서 제외
        * git status : 파일 상태 확인 -> 추적상태
        * git commit -m "--" : 주석 달기
        * git log : 주석 확인
        * git log --oneline : 한줄형태의 주석 확인
        * git log --all --decorate --oneline --grapgh : 모든 브랜치의 로고 보기
        * git checkout --(해시) : 그 당시 커밋의 시점으로 넘어감 파일들도 포함
        ->git checkout main (돌아오기)
        * git reset : git reset --mixed
        * git reset --hard 해시값 : 해당 해시값 이후에 발생한 commit 전부 삭제
          git reset --mixed 해시값 : 해당 해시값 이후로 삭제하지만 파일들은 남김 다시 커밋 하기 위해서는 add 명령어를 입력해야함
          git reset --soft 해시값 : commit 내용만 삭제 다시 commit 하면 사용가능  
        * git reflog : 날아간 commit 이력들을 볼 수 있음
        * git reset --hard 해시값 : commit 들 다시 복구
          (reset 시킨 후 변동 되있는거 일일히 수정해야 함 , 복구시 파일을 완전히 삭제했다면 안에 내용은 복구 불가 커밋 이력만 돌아옴)
        * git revert 해시값 : 해시값의 commit 된 내용들 그전 상태로 전환 ,revert 라는 이력 남음 (오류 발생시 git revert --continue -> git revert --no-commit)

#####Tip

        * .gitignore : 폴더안에 .gitignore 파일명 생성후 그안에 커밋하고 싶지 않은 파일명을 생성하면 그파일은 커밋되지 않는다. 
        (ex) admin_info.yaml < 이 파일은 커밋되지 않는다
        * vim 편집기 : commit시 나올수 있음 쉬프트 i or i + :wq(저장후 종료) q, esc(입력종료) 이정도만 알면 될 듯
        
###Commit 

        * commit은 언제든 생성하고 그곳으로 이동 있으나 협업 시 중요한 곳에만 커밋을 남김

##branch

        * 독립적으로 작업을 시행 할 때 생성 
        * 명령어 
            - git branch : 브랜치 목록 확인
            - git branch 000(브랜치명) : 브랜치생성
            - git switch 000 : 해당 브랜치로 이동
            - git switch -c 000 : 생성과 동시에 브랜치로 이동
            - git branch -d 000 : 해당 브랜치 삭제
            - git branch -m 000(기존이름) 000(변경할이름) : 브랜치명 변경
            - git merge 000(합치고자하는 브랜치) : branch 이력을 유지한체 메인 브랜치에 합치는것, 이력 남음 
                1. git switch main
                2. git merge 000
                3. git log (확인)
                4. git branch -d 000(없앤 브랜치명) : merge후 합친 브랜치명 삭제
                * 2가지 merge 방식
                    1. 3-way-merge
                    메인이 나아가고 메인 이전에 파생된 브랜치에서 메인이랑 합쳐지는 것
                    병합된 브랜치의 커밋 이력과 merge 된 브랜치 이력이 안남음 다음 커밋에 모든내용 집어넣는것
                    2. fast forward 
                    git merge --no -f 0000( 이방식 사용 x)
                5. git merge --squash 000 : commit 이력과 merge된 브랜치 이력도 남기지 않고
                새로운 commit에 상대 브랜치의 내용을 모두 집어넣음 ,자동 커밋되지 않아 별도의 커밋요구
            - git rebase :
                브랜치의 이력을 메인 브랜치와 연걸지어 하나의 이력으로 만들어줌
                기존 브랜치의 이력이 사라지므로 깨끗한 이력을 관리하기 용이
                하나의 이력으로 만드는 과정에서 모든 커밋은 재정렬 되고 기존 로그의 해시값이 변동되어 충돌등의 문제를 야기
                1. git switch 0000
                2. git rebase main
                3. git switch main
                4. git merge 0000
                5. git branch -d 0000
            - git cherry-pick 0000(해시값) : 브랜치에서 원하는 commit 을 가져올 수 있음 
            복사해서 가져오는 것이기에 브랜치의 commit에 영향 없음
            - git --reapply-cherry-pics 0000 : 되돌리기
            * 문제 발생 *
                1. merge 과정에서 같은 파일의 값이 변경된 경우
                그 값중 무슨 값을 선택할지 클릭 한 후 저장 -> git add . -> git commit
                2. rebase 과정에서 같은 파일의 값이 충돌할 경우
                위와 같이 선택 후 -> 파일저장 -> git add. -> git rebase --continue

         
