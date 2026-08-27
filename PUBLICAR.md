# Três comandos para subir

Crie o repositório vazio no GitHub (recomendado: **privado**), depois, dentro desta pasta:

```bash
git init && git add . && git commit -m "Manual e fluxo de publicações do escritório"
git branch -M main
git remote add origin git@github.com:SEU-USUARIO/SEU-REPO.git && git push -u origin main
```

Se usar HTTPS em vez de chave SSH, troque a última linha por:

```bash
git remote add origin https://github.com/SEU-USUARIO/SEU-REPO.git && git push -u origin main
```

Para atualizar depois de qualquer alteração:

```bash
git add . && git commit -m "descreva o que mudou" && git push
```
