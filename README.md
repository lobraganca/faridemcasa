# Farid em Casa — Front-end

Protótipo navegável do novo site/app do **Farid em Casa** (supermercado online, 6 lojas).
Página única (`index.html`), sem build, hospedada na Vercel.

## O que já funciona (no navegador)
- Escolha de cidade/loja com sugestão da loja mais próxima (geolocalização)
- Departamentos, busca (sem acento, sinônimos), ofertas, carrinho
- Agendamento de entrega/retirada (janelas, pedido mínimo R$ 50)
- Login/cadastro **de demonstração**, WhatsApp, botão voltar ao topo

## O que é demonstração (precisa de backend antes de produção)
| Item | Hoje | Produção |
|---|---|---|
| Login/cadastro | simulado no navegador | API de autenticação (OAuth2/OIDC, senha com hash forte, MFA opcional, rate-limit) |
| Catálogo, preços, estoque | dados fixos no HTML | API do e-commerce/ERP atual, por loja |
| Horários de entrega | janelas fixas | API de capacidade logística por loja |
| Pedido/pagamento | não enviado | API de pedidos + gateway PCI-DSS (sem dados de cartão no front) |
| Endereço | salvo só no navegador | API com consentimento (LGPD) |

## Segurança aplicada no front
- Todo texto vindo do usuário é escapado antes de ir para a tela (anti-XSS)
- CPF e celular **não** são guardados no navegador (LGPD)
- `vercel.json` com HSTS, CSP, X-Frame-Options, Referrer-Policy, Permissions-Policy
- Links externos com `rel="noopener"`

## Próximos passos recomendados
1. Migrar para Next.js (componentes + rotas de API) e remover `onclick` inline → CSP sem `unsafe-inline`
2. Integrar APIs reais (catálogo, estoque, pedidos, auth) com variáveis de ambiente na Vercel
3. Testes automatizados (Playwright) e auditoria de acessibilidade (WCAG 2.1 AA)
4. Monitoramento (Vercel Analytics/Logs) e revisão de segurança pela equipe de TI
