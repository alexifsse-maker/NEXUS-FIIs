# NEXUS FIIs — versão 1.0

PWA sem dependências para cadastro manual de FIIs e projeção de reinvestimento.

## Publicar no GitHub Pages

1. Crie um repositório exclusivo chamado `NEXUS-FIIs`. No GitHub Free, use um repositório público para o Pages.
2. Extraia este pacote. Coloque seu conteúdo na raiz do repositório, incluindo a pasta `.github`.
3. Em Settings → Pages → Build and deployment, selecione GitHub Actions.
4. Execute o workflow “Publicar NEXUS FIIs” na aba Actions (ou envie uma alteração para main).
5. Abra o endereço informado no deployment. No Android/Chrome, use a opção de instalar ou adicionar à tela inicial.

Alternativa: publique pela branch main, pasta raiz, nas configurações do Pages. Os arquivos da raiz já estão prontos para servir diretamente. Não precisa de npm ou compilação.

## Como usar

- Carteira: cadastre código, quantidade, preço, dividendo por cota e saldo dedicado a esse fundo. Edite e exclua quando necessário.
- Simulador: escolha um fundo, aporte mensal e horizonte. As simulações não registram compras reais nem alteram a carteira.
- Backup: baixe o JSON completo e guarde em uma pasta privada fora do aparelho; por exemplo, envie manualmente ao Google Drive. Para restaurar, selecione o JSON, revise e confirme.
- Recuperação local: retorna à versão anterior à última alteração. Não substitui backup externo.

## Regras de cálculo

- Dividendo mensal = quantidade × dividendo por cota, arredondado para centavos por fundo.
- Próxima cota: número inteiro de pagamentos mensais necessário para completar seu preço, considerando saldo atual e renda constante, sem aporte. Se o saldo já cobre o preço, mostra disponibilidade imediata.
- Cotas para comprar uma cota por mês = teto(preço / dividendo por cota).
- Projeção: recebe dividendos das cotas existentes, soma o aporte no fim do mês, compra cotas inteiras e mantém a sobra. As cotas novas rendem no mês seguinte. Um saldo que já permite compras é aplicado ao final do primeiro mês na simulação.
- Preços, dividendos e aportes constantes. Não inclui taxas, impostos nem oscilação de mercado.
- Saldo é reservado por fundo. Não repita um mesmo saldo em vários cadastros.

## Dados e privacidade

O app começa vazio. Os valores de teste usados na validação não estão neste pacote.
Dados ficam no localStorage do navegador; não vão para o GitHub. O site e seu código são públicos quando publicados em Pages público. Não há login, sincronização entre aparelhos ou backup automático em nuvem. Backups JSON não são criptografados.

Os dados pertencem à origem do endereço. Trocar de domínio, navegador ou aparelho exige exportar e restaurar. Faça backup antes de trocar endereço. Mantenha cada app NEXUS em origem separada quando isolamento de segurança for necessário: sites no mesmo domínio compartilham acesso ao localStorage.

## Offline e atualizações

Após abrir com internet em HTTPS e instalar o cache, o app pode funcionar offline. O botão de instalação depende do navegador; use o menu do Chrome se ele não aparecer. Em atualizações, incremente CACHE em sw.js; mantenha as chaves de dados e faça migrações compatíveis. Não apague os dados do navegador como rotina de atualização.

## Verificação desta entrega

Verificados: sintaxe JavaScript; cálculo da próxima cota; compras inteiras; saldo residual; rendimento de cotas novas no mês seguinte; aporte; validação de valores e duplicidade; ida e volta do JSON. No navegador: cadastro, edição, persistência ao recarregar, simulação e acionamento da exportação.

Pendente em endereço HTTPS real/aparelho: instalação PWA, funcionamento offline, download/restauração pelo seletor de arquivos do Android e atualização do service worker. A prévia HTTP de desenvolvimento não permite validar instalação ou offline.
