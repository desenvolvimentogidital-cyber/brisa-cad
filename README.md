# Briza CAD 2.4.1

Editor CAD 2D vetorial para a Web, construído em React/Next.js e preparado para deploy na Vercel.

## Estado

A versão 2.4.1 é um **beta técnico para validação online**. O núcleo CAD possui testes automatizados para geometria, DXF, arquitetura, migração, blocos, snaps, constraints e desempenho. Consulte:

- `REVISAO-COMPLETA-2.4.1.md` — auditoria e lacunas conhecidas;
- `CHECKLIST-TESTES.md` — roteiro completo de validação manual;
- `CAD-PRO-STATUS.md` — evolução funcional do CAD;
- `IMPLEMENTACAO-2.4.0.md` — histórico da rodada anterior.

## Principais recursos

- linhas, polilinhas, retângulos, círculos, arcos, elipses, polígonos, splines/NURBS e textos;
- move/copy/rotate/scale/mirror/offset/trim/extend/break/stretch/align/join/fillet/chamfer/arrays;
- seleção window/crossing/polygon/fence, grips, Quick Select, Match Properties e isolate;
- snaps avançados, ORTHO e POLAR;
- layers, linetypes, lineweights e layer states;
- blocos, hachuras, cotas associativas e constraints;
- paredes, portas/janelas hospedadas, pilares, vigas, coberturas, escadas, ambientes e quantitativo;
- autosave, backup, recuperação e migração de documentos antigos;
- DXF, SVG, impressão/PDF e prancha técnica;
- DWG opcional via conversor server-side;
- benchmark automatizado com 50 mil entidades.

## Requisitos

- Node.js 22.13 ou superior;
- npm compatível com o `package-lock.json`.

## Desenvolvimento local

```bash
npm ci
npm run dev
```

Abra o endereço informado pelo Next.js.

## Validação

```bash
npm run typecheck
npm run lint
npm run test:core
npm run build
npm run test:smoke
```

Ou execute tudo:

```bash
npm run check
```

## Vercel

O repositório está configurado como projeto Next.js nativo. Na Vercel:

1. importe o repositório GitHub;
2. Framework Preset: **Next.js**;
3. Install Command: `npm ci`;
4. Build Command: `npm run build`;
5. nenhuma variável é obrigatória para DXF e demais recursos locais;
6. depois do deploy, acesse `/api/health` para confirmar a versão.

### Conversão DWG opcional

Para habilitar DWG, configure na Vercel:

```text
DWG_CONVERTER_URL=https://seu-conversor.example/convert
DWG_CONVERTER_TOKEN=token-opcional
```

O endpoint externo deve receber `multipart/form-data` com `file` e devolver DXF como texto. As variáveis ficam no servidor e não são expostas no bundle do navegador.

## Persistência

O autosave atual é local ao navegador (`localStorage`) e existe exportação/importação de projeto. Publicar na Vercel **não sincroniza projetos entre dispositivos**. Sincronização multiusuário exige uma futura camada de autenticação + banco/storage.

## CI

`.github/workflows/ci.yml` valida automaticamente:

- `npm ci`;
- TypeScript;
- ESLint;
- testes de núcleo;
- build Next.js de produção;
- smoke test do servidor e `/api/health`.

## Licença

Software proprietário. Consulte `LICENSE`.
