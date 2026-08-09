# pr-playground

여러 계정이 얽힌 협업 흐름을 연습하는 저장소.

저장소 소유자와 작업자가 다를 때 권한이 어떻게 동작하는지, 협업자 초대와 수락이 어떤 순서로 이뤄지는지, 리뷰어를 지정한 PR이 어떻게 흘러가는지를 실제로 눌러보며 확인합니다.

## 정리

- 소유자가 아닌 계정이 PR을 올리고 머지까지 하려면 **write 권한**이 필요하다. 초대는 소유자가 보내고, 받는 쪽이 수락해야 실제로 붙는다.
- 리뷰어를 지정해도 승인 없이 머지는 가능하다. 이를 막으려면 **branch protection rule**에서 필수 승인 수를 걸어야 한다.
- `--delete-branch`를 붙이면 머지와 동시에 원격 브랜치가 정리된다.

```bash
gh api -X PUT repos/<owner>/<repo>/collaborators/<user> -f permission=push
gh api user/repository_invitations                 # 받는 쪽에서 초대 확인
gh api -X PATCH user/repository_invitations/<id>   # 수락

gh pr create --reviewer <user> --title "..." --body "..."
gh pr merge <번호> --merge --delete-branch
```
