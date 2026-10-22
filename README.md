# Panetonne Android — primeira base (v0.1.0)

Projeto Android nativo em Kotlin + Jetpack Compose, preparado a partir do protótipo Python enviado. Esta é uma **base de desenvolvimento**, não um APK já compilado/testado.

## O que já está implementado

- Interface de chat escura com identidade visual Panetonne.
- Alternância entre modo local básico e modo online.
- Persistência local privada de histórico e memória usando SharedPreferences/JSON.
- Migração das quatro lembranças iniciais do `memoria.txt` original para a primeira inicialização.
- Tela para visualizar/editar a memória (uma entrada por linha).
- Comando de conversa `Lembre que ...` / `Lembra que ...` / `Guarde que ...` para adicionar uma lembrança.
- Busca simples por termos na memória quando offline.
- Integração opcional com endpoints HTTPS compatíveis com o formato OpenAI Chat Completions.
- Endpoint, nome do modelo e chave configuráveis pelo usuário; nenhuma chave vem embutida no código.
- Mensagens de erro básicas para falhas de rede e respostas HTTP inválidas.

## Limitações conhecidas desta versão

1. O modo local **não é ainda um modelo de linguagem**: consulta memória e responde com regras simples. Portanto, não tem a capacidade de raciocínio de um LLM offline.
2. O modo online exige um endpoint compatível e, dependendo do provedor, uma chave de API. Não existe um servidor online gratuito incluído neste projeto.
3. A chave é guardada nas preferências privadas do aplicativo, mas ainda não usa Android Keystore. Não compartilhe o aparelho com pessoas não confiáveis se salvar uma chave.
4. O histórico é limitado às últimas 100 mensagens salvas e a requisição online usa até 12 mensagens recentes.
5. Ainda não há backup/importação, voz, pesquisa web, leitura de PDFs, modelo local real nem testes automatizados. São etapas seguintes.
6. Não foi possível compilar ou executar um APK neste ambiente porque não há Android SDK/Gradle instalados. O projeto precisa ser sincronizado e compilado no Android Studio ou em um ambiente Android configurado.

## Requisitos de compilação

- Android Studio recente com suporte a Kotlin 2.0 e Android Gradle Plugin 8.7.x.
- JDK 17 (o ambiente do Android Studio costuma gerenciá-lo).
- Android SDK Platform 35 e Build Tools compatíveis.
- Acesso à internet na primeira sincronização do Gradle para baixar dependências.
- Dispositivo Android 8.0 (API 26) ou superior para instalação.

## Como gerar o APK

1. Extraia a pasta `PanetonneAndroid`.
2. Abra essa pasta no Android Studio usando **Open**.
3. Aceite a sincronização do Gradle e instale os componentes do SDK que forem solicitados.
4. Aguarde a sincronização terminar e resolva qualquer aviso de versão de SDK.
5. Use **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
6. O APK de depuração normalmente será criado em `app/build/outputs/apk/debug/app-debug.apk`.
7. Copie o APK para o celular e instale-o. O Android pode pedir autorização para instalar apps dessa origem.

Se houver erro de compilação, copie o primeiro erro real da janela Build (não apenas as últimas linhas) para diagnosticar.

## Configurar a IA online

Na aplicação, abra Configurações e informe:

- Endpoint HTTPS completo que aceite `POST` com JSON no formato `{"model":"...","messages":[...]}` e retorne `choices[0].message.content`.
- Nome do modelo aceito pelo serviço.
- Chave de API, se o serviço exigir.

O projeto não inclui um endpoint ou uma chave. Não use endpoints HTTP sem TLS. Para distribuição pública, prefira um backend intermediário e não embuta segredos no APK.

## Próximas etapas recomendadas

1. Adicionar exportação/importação de backup com validação e confirmação antes de mesclar/substituir dados.
2. Migrar armazenamento para Room/SQLite e criar testes de persistência.
3. Proteger credenciais com Android Keystore e melhorar a tela de configuração.
4. Integrar um modelo local pequeno e quantizado, avaliando RAM, armazenamento, consumo e licença do modelo.
5. Implementar provedor online com tratamento de privacidade, limites e indicação clara de quando os dados saem do dispositivo.
6. Acrescentar documentos, pesquisa com fontes, voz e permissões explícitas para ferramentas.
7. Testar em aparelhos reais e automatizar a geração de APK.

## Arquivos de origem preservados

`docs/memoria-original-preservada.txt` contém uma cópia exata da memória inicial fornecida. A aplicação usa as mesmas quatro informações para inicializar a memória na primeira execução.
