# Como publicar seu README animado

## 1. Crie o repositório especial
No GitHub, crie um repositório **público** com o nome exatamente igual ao seu usuário
(ex.: `gustavo10887/gustavo10887`). O GitHub mostra o README dele no seu perfil.

> Se seu usuário não for `gustavo10887`, troque em 3 lugares:
> `data/profile_info.json` ("username"), `README.md` (os dois `<code>`) e
> `.github/workflows/update-profile-art.yml` (linha `GH_PROFILE_USER`).

## 2. Gere o retrato em ASCII (no seu computador)
Coloque uma foto sua (rosto, fundo simples) na raiz da pasta como `source-photo.png` e rode:

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate    |   Linux/Mac: source .venv/bin/activate
pip install -r scripts/requirements.txt
pip install rembg "onnxruntime>=1.16.0" opencv-python   # remove o fundo da foto

python scripts/prep_photo.py source-photo.png source-prepped.png
# Windows PowerShell: $env:GH_PROFILE_USER="gustavo10887"
export GH_PROFILE_USER="gustavo10887"
python scripts/make_ascii_svg.py
```

Isso cria o `ascii-portrait.svg`. (O `info-card.svg` já está pronto; se editar
`data/profile_info.json`, rode `python scripts/make_info_card.py` de novo.)

## 3. Envie tudo para o repositório
```bash
git init
git add .
git commit -m "feat: README animado do perfil"
git branch -M main
git remote add origin https://github.com/gustavo10887/gustavo10887.git
git push -u origin main
```

## 4. Libere o GitHub Actions
No repositório: **Settings → Actions → General → Workflow permissions →
"Read and write permissions"** → Save. Depois vá em **Actions → Update profile art →
Run workflow**. A partir daí o gráfico de contribuições se atualiza sozinho todo dia.

Dica: em **Settings do perfil → Public profile**, marque "Include private contributions"
para o gráfico contar também commits em repositórios privados.
