### なぜ今更
https://applech2.com/archives/20190604-zsh-as-the-default-shell-on-macos-10-15-catalina.html  
次のMAC OS catalinaからデフォルトがzshになるらしいので  
(新規ユーザのみで既存ユーザは変わらないけどmacユーザ貫く予定なので)

bash
PS1=`[\t]yanada: \w/$`

zsh
PS1=`[%*]yanada: %~/$ `

こんな感じの表示 `[18:05:46]yanada: ~/$`

Tabの補完が神
  でもbashに慣れてるとついついtab連打しちゃう
  



この辺みた
https://qiita.com/yamagen0915/items/77fb78d9c73369c784da
