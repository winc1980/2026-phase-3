# issueに着手してからPRを出すまで
1. mainを最新にする
```bash
git switch main
git pull origin main
```
2. 作業用ブランチを切る（例: issue #12 なら `feature/12-login`）
```bash
git switch -c feature/12-login
```
> 💡 ブランチを切ると、mainを壊さずに試行錯誤でき、変更がissue単位でまとまるのでレビューもしやすくなります。

3. 作業して、区切りごとにコミット
```bash
git status                          # 変更したファイルを確認
git add .
git commit -m "ログイン画面を追加 #12"
```
4. リモートにpush（2回目以降は `git push` だけでOK）
```bash
git push -u origin feature/12-login
```
5. GitHubで「Compare & pull request」→ 説明欄に `closes #12` と書いてPRを作成（マージ時にissueが自動で閉じる）

# チームメンバーのPRをレビューするとき
1. 自分のブランチに作業途中の変更があれば、一時退避する
```bash
git stash -u                        # -u: 新規ファイルも含めて退避
```
2. レビュー対象のブランチを取得して切り替える
```bash
git fetch origin
git switch feature/15-signup
```
3. 動作確認し、GitHubの「Files changed」でコメント → Approve / Request changes
4. 自分のブランチに戻り、退避した変更を復元する
```bash
git switch feature/12-login
git stash pop
```
