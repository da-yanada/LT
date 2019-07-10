# bashからzshに(今更)乗り換えた話

## なぜ今更
次のMAC OS catalinaからデフォルトがzshになるらしいので、そろそろ変えようかなと  
(新規ユーザのみで既存ユーザは変わらない)

https://applech2.com/archives/20190604-zsh-as-the-default-shell-on-macos-10-15-catalina.html  

## やった手順
### インストール
持っているMAC OSには元から入ってました

### 設定

#### zsh用のrcファイルを作成、.bashrcにaliasなど書いていたので、全てそのままコピー
- `cat ~/.bash_profile >> ~.zshrc`
- `cat ~/.bashrc >> ~/.zshrc`




#### コマンドラインの左に表示されるところを編集
- MACのデフォルト `ユーザー名noMacbook:~ ユーザー名$ `
  - noMacbookとかいらない。
  - カレントディレクトリしか出なくてたまにどこにいるか分からなくなる
- もともとこう変更してた
  - `[18:05:46]yanada: ~/$`
  - やり方は、PS1=`[\t]yanada: \w/$`  
    PS1という環境変数を書き換えると変わる。  
     `\t`で今の時間 `\w`でカレントディレクトリのフルパス  
     `[今の時間]yanada: フルパス$ `と言った感じ
     
でもzshにすると、そのまま`[\t]yanada: \w/$`という文字列で表示されてしまったので  
zshに対応した書き方に変更  

変更後　→ PS1=`[%*]yanada: %~/$ `  
この変更を.zshrcにも反映。

これで今まで通り`[18:05:46]yanada: ~/$`になった

#### historyを残すように設定
bashだと、今までは↑キーを押して直近のコマンドを出したり  
historyコマンドで過去のコマンドの履歴を表示したり出来たが
zshだと設定をしないと出来ないらしいので.zshrcに追加
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

#### chshでログインシェルを変更
- `chsh -s /usr/local/bin/zsh`

これでターミナルを開いた際にデフォルトでzshになる

### 使ってみた感想
#### goodなところ
Tabの補完が神
  でもbashに慣れてるとついついtab連打しちゃう
  
### 困ったこと
基本、linuxはbashがデフォルトなので、サーバ作業の時にちょっと都合が違ってうーんってなる

### 最後に
まだ使い始めてまもないので、まだまだ使いこなせてません。
zshのうまい使い方教えてください。

### この辺みた
https://qiita.com/yamagen0915/items/77fb78d9c73369c784da
https://gist.github.com/d-kuro/352498c993c51831b25963be62074afa
