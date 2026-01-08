# Manual Operacional — ZEDCAM (Museu do Futebol)

> Uso interno | Operação do sistema 

## 1) Visão geral

Este aplicativo utiliza uma câmera **ZED** para fazer *body tracking* e animar um esqueleto na Unity.  
Uma **camiseta** (mesh) é acoplada ao esqueleto e é a **única parte 3D renderizada**.  
Em seguida, o output da câmera recebe um efeito de **chroma key** para recortar o fundo real e exibir a pessoa em um **background “fake”** (imagem).

---

## 2) Conexões e cabos (obrigatório)

Conecte os dispositivos exatamente assim:

- **Projetor:** HDMI  
- **Monitor:** DisplayPort **e** USB-C  
- **Câmera ZED:** USB **3.0** (porta azul)

**Importante:** Se a ZED estiver em USB 2.0, o tracking pode ficar instável e/ou falhar ao iniciar.

---

## 3) Builds diferentes por máquina (orientação da ZED)

Cada máquina tem uma **build diferente**, porque a **orientação física** da ZED (lado/rotação) varia entre os PCs.

### Como identificar PC invertido (build errada no PC)
- Se a **pessoa** (recorte do chroma) estiver **de ponta cabeça em relação ao fundo** e o enquadramento do chroma estiver errado, **provavelmente os PCs estão invertidos** (build do PC A rodando no PC B).

### Quando é apenas rotação do Windows
- Se **tudo** estiver de ponta cabeça junto (pessoa, fundo e UI), normalmente basta ajustar a **rotação de tela no Windows** (Configurações > Sistema > Tela > Orientação).


---

## 4) Telas invertidas (monitor/projetor)

Se a imagem do monitor e do projetor estiverem trocadas:

- **Tecla `E`**: inverte as saídas (**monitor ↔ projetor**)

---

## 5) Tracking ruim: limpeza e ferramentas do ZED SDK

Se o tracking estiver ruim (perda de esqueleto, tremores, offsets estranhos):

1. Limpe a lente da ZED com pano de microfibra (sem produtos abrasivos).
2. Use os apps do **ZED SDK** instalados na máquina para validar a câmera (ex.: ZED Explorer / ZED Diagnostic).
3. Se houver motivo claro, use o **ZED Calibration** (recalibração).

### Links oficiais (Stereolabs)
- ZED Explorer: https://www.stereolabs.com/docs/development/zed-tools/zed-explorer
- ZED Diagnostic: https://www.stereolabs.com/docs/development/zed-tools/zed-diagnostics
- ZED Calibration: https://www.stereolabs.com/docs/development/zed-tools/zed-calibration
- Instalação do ZED SDK no Windows: https://www.stereolabs.com/docs/development/zed-sdk/windows
- Página de releases do ZED SDK: https://www.stereolabs.com/developers/release

> ⚠️ Nota: a calibração de fábrica normalmente é mais precisa. Recalibre somente se houver motivo (impacto, vidro na frente da lente, etc.).

---

## 6) Troca do fundo (background)

Para alterar o fundo exibido (imagem do background fake):

1. Feche o aplicativo (recomendado).
2. Vá até:  
   `PastaDaBuild/ZEDCAM_MuseudoFutebol_Data/StreamingAssets/BackgroundTextures`
3. Substitua a imagem existente **ou** coloque a imagem desejada como a **primeira** da pasta.
4. **IMPORTANTE:** apenas a **primeira** imagem da pasta será exibida.
5. Se a orientação do fundo aparecer errada, pode ser necessário **girar a imagem 180 graus** antes de salvar.

Recomendações:
- Formato: PNG ou JPG
- Evite nomes com caracteres especiais

---

## 7) Catálogo de camisetas (texturas)

Para adicionar/remover/editar camisetas (basecolors):

1. Feche o aplicativo (recomendado).
2. Vá até:  
   `PastaDaBuild/ZEDCAM_MuseudoFutebol_Data/StreamingAssets/ShirtTextures`
3. Adicionar, remover ou editar qualquer imagem nessa pasta muda o **catálogo de camisetas disponíveis**.
4. Abra o app e verifique se aparece corretamente.

Boas práticas:
- Faça backup das texturas antes de substituir.
- Mantenha o mesmo tamanho de imagem entre as texturas para consistência.

---

## 8) Template PSD (criação de camisetas)

Existe um PSD com um template pronto com:
- Partes marcadas (gola, manga, barra)
- Padronagens prontas (visibilidade e cor ajustáveis)
- Uma imagem da **UV do modelo** dentro do PSD para referência


### Como usar (resumo)
1. Abra o PSD e duplique a arte/base para uma nova variação.
2. Ative/desative padronagens e ajuste cores para chegar no visual desejado.
3. Use a UV como guia se quiser criar uma padronagem alinhada ao modelo.
4. Exporte (PNG/JPG) e coloque em `StreamingAssets/ShirtTextures`.

---
