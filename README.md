# 📚 Guia de Trabalho Colaborativo com Branches Git

Este guia descreve o fluxo de trabalho recomendado para equipes que desenvolvem em paralelo utilizando branches derivadas da branch `developer`.

## 🧱 Estrutura de Branches

- `main`: branch principal, contém apenas código estável e pronto para produção.
- `developer`: branch de integração, reúne todas as funcionalidades em desenvolvimento.
- `nome-da-ação/funcionalidade`: branches individuais para cada nova funcionalidade ou ajuste.

## ✅ Passo a Passo: Trabalhando com Branches Paralelas

### 1. Atualize a branch `developer` antes de iniciar

git checkout developer
git pull origin developer
git checkout -b ação/minha-feature-xyz

> 🔁 Substitua `ação/minha-feature-xyz` pelo nome da sua feature branch.

### 2. Faça as alterações normalmente na sua branch

git add .
git commit -m "feat: implementa nova funcionalidade"
git push origin ação/minha-feature-xyz

### 3. Atualize sua branch com a `developer` antes de criar um Pull Request

# Atualize a developer
git checkout developer
git pull origin developer

# Volte para sua branch de feature
git checkout ação/minha-feature-xyz

# Integre as atualizações da developer com sua branch ação/minha-feature-xyz
git merge developer
# ou, se preferir histórico linear:
# git rebase developer

> ⚠️ Resolva conflitos se houver, teste novamente e faça push:

git push origin ação/minha-feature-xyz

### 4. Abra um Pull Request para a `developer`

- Crie um PR da sua branch (`ação/minha-feature-xyz`) para a branch `developer`.
- Solicite revisão de outro membro da equipe.
- Após aprovação, o código é mesclado na `developer`.

### 5. No próximo dia de trabalho, mantenha sua branch sincronizada

git checkout developer
git pull origin developer
git checkout ação/minha-feature-xyz
git merge developer

> 💡 Isso garante que sua branch local esteja sempre atualizada com o que há de mais recente na `developer`.

---

## 🔄 Lidando com Alterações Não Commitadas (Uso do `git stash`)

**Princípio:** não trabalhe diretamente em `main` ou `developer`. Trabalhe em branches de feature. `git stash` é um recurso temporário para salvar trabalho em progresso.

### 🟢 Fluxo recomendado — você está na sua branch de feature (ex.: `feat/emerson-x`)

git stash                    # guarda alterações locais (se houver)
git pull origin developer    # traz novidades da developer para sua branch atual
git stash apply              # reaplica e mantém a stash (ou use git stash pop para reaplicar e remover a stash)
# resolva conflitos, depois git add e git commit

### 🟢 Se você acidentalmente editou em `developer`

**Opção A (melhor): crie uma branch e commit**

git checkout -b feat/nova-tarefa   # cria branch mantendo as alterações
git add .
git commit -m "WIP: inicia tarefa X"
# agora atualize developer se necessário:
git checkout developer
git pull origin developer

**Opção B (com stash)**

git stash
git pull origin developer
git checkout -b feat/nova-tarefa
git stash pop
# resolva conflitos, git add, git commit

### 🟢 Diferença entre apply e pop

- `git stash apply` — reaplica a stash, mas **mantém** a entrada no stash list.
- `git stash pop` — reaplica **e remove** a stash.

Use `git stash list` para ver stashes e `git stash drop` para removê-las manualmente.

---

## 🔖 Convenções de Nome de Branch

Utilize nomes de branch claros e padronizados:

| Prefixo     | Significado                    | Exemplo                         |
|-------------|--------------------------------|----------------------------------|
| `feat/`     | Nova funcionalidade            | `feat/fulano-login`             |
| `fix/`      | Correção de bug                | `fix/ciclano-menu-responsivo`   |
| `refactor/` | Refatoração de código          | `refactor/beltrano-limpar-codigo`|

## ✔️ Boas Práticas

- **Não trabalhe diretamente nas branches `main` ou `developer`.**
- **Crie Pull Requests pequenos e focados.**
- **Atualize sua branch com frequência.**
- **Sempre revise o código dos colegas.**
- **Escreva mensagens de commit claras.**

> Este fluxo permite que a equipe trabalhe com segurança, paralelismo e organização, minimizando conflitos e mantendo o projeto sustentável.
