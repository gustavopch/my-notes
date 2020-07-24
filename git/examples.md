# Git: Exemplos

- **`git add my-file.js`: Adiciona o arquivo `my-file.js` ao stage.**
- `git add . `: Adiciona todos os arquivos do diretório atual ao stage.
- `git add -p`: Entra num modo interativo em que o Git te mostra cada modificação e pergunta se quer adicionar ao stage, ignorar, etc.
- `git add -p my-file.js`: Mesmo do `git add -p`, porém apenas no arquivo `my-file.js`.
- **`git commit`: Cria um commit com as alterações que estão no stage.**
- `git commit -m "Update README.md"`: Mesmo do `git commit`, porém já especifica que o título do commit será "Update README.md".
- `git commit --amend`: Emenda o commit atual (note que commits são imutáveis e, na prática, você estará criando um novo commit com um novo hash).
- **`git rebase master`: Copia cada commit do branch atual pro branch `master`.**
- `git rebase master new-button`: Copia cada commit do branch `new-button` pro branch `master`.
- **`git stash`: Salva as modificações locais do código em um novo stash e limpa seu diretório de trabalho.**
- `git stash list`: Mostra a lista de stashes.
- `git stash pop`: Traz o último stash salvo de volta pro diretório de trabalho.
- `git stash -u`: Mesmo do `git stash`, porém também vai salvar os arquivos que ainda não estão sendo rastreados pelo Git (`-u` de "untracked").
- `git stash pull -m "My stash message"`: Mesmo do `git stash`, porém o stash resultante será nomeado "My stash message" ao invés do nome automático definido pelo Git.