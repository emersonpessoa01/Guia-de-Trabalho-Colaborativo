# 📚 Guia de Trabalho Colaborativo com Branches Git

Este guia descreve o fluxo de trabalho recomendado para equipes que desenvolvem em paralelo utilizando branches derivadas da branch `developer`.

## 🧱 Estrutura de Branches

- `main`: branch principal, contém apenas código estável e pronto para produção.
- `developer`: branch de integração, reúne todas as funcionalidades em desenvolvimento.
- `feat/<nome-dev>-<descricao>`: branches individuais para cada nova funcionalidade ou ajuste.

## ✅ Passo a Passo: Trabalhando com Branches Paralelas

### 1. Atualize a branch `developer` antes de iniciar

```bash
git checkout developer
git pull origin developer
git checkout -b stefany/minha-feature-xyz
```

> 🔁 Substitua `stefany/minha-feature-xyz` pelo nome da sua feature branch.

### 2. Faça as alterações normalmente na sua branch

```bash
git add .
git commit -m "feat: implementa nova funcionalidade"
git push origin stefany/minha-feature-xyz
```

### 3. Atualize sua branch com a `developer` antes de criar um Pull Request

```bash
# Atualize a developer
git checkout developer
git pull origin developer

# Volte para sua branch de feature
git checkout stefany/minha-feature-xyz

# Integre as atualizações da developer com sua branch stefany/minha-feature-xyz
git merge developer
# ou, se preferir histórico linear:
# git rebase developer
```

> ⚠️ Resolva conflitos se houver, teste novamente e faça push:

```bash
git push origin stefany/minha-feature-xyz
```

### 4. Abra um Pull Request para a `developer`

- Crie um PR da sua branch (`stefany/minha-feature-xyz`) para a branch `developer`.
- Solicite revisão de outro membro da equipe (ex: Emerson).
- Após aprovação, o código é mesclado na `developer`.

### 5. No próximo dia de trabalho, mantenha sua branch sincronizada

```bash
git checkout developer
git pull origin developer
git checkout stefany/minha-feature-xyz
git merge developer
```

> 💡 Isso garante que sua branch local esteja sempre atualizada com o que há de mais recente na `developer`.

## 🔖 Convenções de Nome de Branch

Utilize nomes de branch claros e padronizados:

| Prefixo     | Significado                    | Exemplo                         |
|-------------|--------------------------------|----------------------------------|
| `feat/`     | Nova funcionalidade            | `feat/emerson-login`            |
| `fix/`      | Correção de bug                | `fix/stephany-menu-responsivo`  |
| `refactor/` | Refatoração de código          | `refactor/emerson-limpar-codigo`|

## ✔️ Boas Práticas

- **Não trabalhe diretamente nas branches `main` ou `developer`.**
- **Crie Pull Requests pequenos e focados.**
- **Atualize sua branch com frequência.**
- **Sempre revise o código dos colegas.**
- **Escreva mensagens de commit claras.**

> Este fluxo permite que a equipe trabalhe com segurança, paralelismo e organização, minimizando conflitos e mantendo o projeto sustentável.
