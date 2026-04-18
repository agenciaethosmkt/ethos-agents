---
step: "03"
name: "Aprovação do Ângulo"
type: checkpoint
depends_on: step-02
outputFile: output/angulo-selecionado.yaml
---

# Step 03 — Checkpoint: Seleção de Ângulo

## Para o Pipeline Runner

Apresentar os 3 ângulos gerados e aguardar seleção humana.

---

Revisar os ângulos em `output/angulos.md`.

**Escolha um ângulo para o criativo:**

1. Ângulo 1 — [Nome]
2. Ângulo 2 — [Nome]
3. Ângulo 3 — [Nome]

Você também pode:
- Combinar elementos de dois ângulos (ex: "1 mas com o hook do 3")
- Pedir um ângulo novo com direção diferente
- Ajustar o hook ou o CTA de um ângulo antes de prosseguir

Após a seleção, salvar em `output/angulo-selecionado.yaml`:

```yaml
angulo_escolhido: 1        # número do ângulo
nome: ""
vetor: ""
hook: ""
desenvolvimento: ""
cta: ""
formato_confirmado: ""
ajustes_usuario: ""        # qualquer ajuste pedido pelo humano
```
