# bashからzshに乗り換えた話

## なぜ今更
次のMAC OS catalinaからデフォルトがzshになるらしいので、そろそろ変えようかなと  
(新規ユーザのみで既存ユーザは変わらない)

Catalinaの詳細はここが詳しく書いてくれている  
https://applech2.com/archives/20190604-macos-10-15-catalina.html   
itunesがなくなるのとか結構衝撃

## zshとは
shellの一つ

bourne　shell系コマンドとcsh系のコマンドが両方使える上に、ksh系のコマンドライン編集機能も実装された究極のシェル。  
らしい。  

とにかくコマンドライン作業を快適に操作できるshell

## やった手順
### インストール
持っているMAC OSには元から入ってました

入っていない場合は  
`brew install zsh`  
`echo /usr/local/bin/zsh >> /etc/shells`

### 設定
#### zsh用のrcファイルを作成、.bashrcにaliasなど書いていたので、全てそのままコピー
- `cat ~/.bash_profile >> ~.zshrc`
- `cat ~/.bashrc >> ~/.zshrc`


#### コマンドラインの左に表示されるところを編集
- MACのデフォルト `ユーザー名noMacbook:~ ユーザー名$ `
  - noMacbookとかいらない。
  - カレントディレクトリしか出なくてたまにどこにいるか分からなくなる
- PS1という環境変数を書き換えると変わる  
  もともとこんな風に表示していた。
  - `[18:05:46]yanada: ~/$`
  - 内容は、PS1=`[\t]yanada: \w/$`  
     `\t`で今の時間 `\w`でカレントディレクトリのフルパス  
     `[今の時間]yanada: フルパス$ `と言った感じ
     
でもzshにすると、そのまま`[\t]yanada: \w/$`という文字列で表示されてしまったので  
zshに対応した書き方に変更  

* 変更後 → PS1=`[%*]yanada: %~/$ `  

この変更を.zshrcにも反映。

これで今まで通り`[18:05:46]yanada: ~/$`になった

けどもうちょっとイケてる表示にしたいなと考え中

#### historyを残すように設定
bashだと、今までは↑キーを押して直近のコマンドを出したり  
historyコマンドで過去のコマンドの履歴を表示したり出来たが  
zshだと設定をしないと出来ないらしいので以下を.zshrcに追加
```
# 履歴ファイルの保存先
export HISTFILE=${HOME}/.zsh_history

# メモリに保存される履歴の件数
export HISTSIZE=1000

# 履歴ファイルに保存される履歴の件数
export SAVEHIST=100000

# 重複を記録しない
setopt hist_ignore_dups

# 開始と終了を記録
setopt EXTENDED_HISTORY
```


#### 補完機能を有効にする
```
# 補完機能有効にする
echo "autoload -U compinit" >> ~/.zshrc
echo "compinit -u " >> ~/.zshrc
```

これで、コマンドを打った後の補完機能が有効になる  
例えば  
`git che`と入力した後にTabを押すと、gitコマンドの中のcheから始まるコマンド一覧が表示され  
もう1度Tabを押すと補完してくれる

```
[11:03:28]yanada: ~/$ git che
check-attr       -- display gitattributes information
check-ignore     -- debug gitignore/exclude files
check-mailmap    -- show canonical names and email addresses of contacts
check-ref-format -- ensure that a reference name is well formed
checkout         -- checkout branch or paths to working tree
checkout-index   -- copy files from index to working directory
cherry           -- find commits not merged upstream
cherry-pick      -- apply changes introduced by some existing commits
```
checkoutの綴りをど忘れしてもこれですぐ表示できる上にtabだけで補完もしてくれる

#### コマンド訂正機能を有効にする
`echo "setopt correct" >> ~/.zshrc`
コマンドのタイプミスをした際に、似たコマンドをサジェストしてくれる。  
その後yを入力するとサジェストされたコマンドを実行できる

#### 移動したディレクトリを記録しておく。"cd -[Tab]"で移動履歴を一覧
`echo "setopt auto_pushd" >> ~/.zshrc`

cdの履歴を覚えてくれる。  
cd -[Tab]と押すと一覧表示される。超便利

#### bashとのお別れ。chshでログインシェルを変更
- `chsh -s /usr/local/bin/zsh`

これでターミナルを開いた際にデフォルトでzshになる

### 使ってみた感想
#### goodなところ
Tabの補完が神
  でもbashに慣れてるとついついtab連打しちゃう
  
#### 困ったこと
基本、linuxはbashがデフォルトなので、サーバ作業の時にちょっと都合が違ってうーんってなる

### 最後に
まだ使い始めたばかりなので、まだまだ使いこなせてません。
zshのうまい使い方教えてください。

### この辺みた
https://qiita.com/yamagen0915/items/77fb78d9c73369c784da
https://gist.github.com/d-kuro/352498c993c51831b25963be62074afa
https://qiita.com/munazo/items/fa010d9815a04578658c
