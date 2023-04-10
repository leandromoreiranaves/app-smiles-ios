'
# Smiles - APP iOS

Aplicativo Smiles desenvolvido em código nativo utilizando Swift e alguns mecanismos em Objective-C.


### Especificações Técnicas

| Descrição     | Valor                   |
| ------------- |------------------------:|
| IDE           | xCode 11.2 (11B52)     |
| Target        | iOS 9 ou Superior       |
| Linguagem     | Swift 5                 |
| Interface     | Storyboard + AutoLayout |


### Estrutura do projeto

* __Root__: Arquivos padrão de projeto como AppDelegate, Info.plist e Assets
* __UI__: Storyboards de interface, xibs, views e view controllers
* __Services__: Arquivos de models e controladoras de acesso ao serviços da api
* __Common__: Libraries, singletons e extensions
* __Resouces__: Imagens, fontes, arquivo de configuração e strings de localização

### Executando o projeto

A execução do projeto é o padrão da plataforma iOS. 
Necessário realizar download das dependências do projeto usando o Pod Install.
```
pod install
```
Ou também é possível utilizar o comando abaixo:
```
pod install --repo-update
```

Caso ocorra algum problema na instalação dos pacotes, como por exemplo o pacote `OpenSSLBitcode`, execute os comandos do CocoaPods na versão `1.2.0`. 

Siga os passos abaixo no terminal: 

###### Remova qualquer versão do CocoaPods
```
sudo gem uninstall cocoapods-downloader
```
###### Instale a versão especifica
```
sudo gem install cocoapods-downloader -v 1.2.0
```

Após estes passos execute o projeto normalmente.


### Dados para testes

| Usuário     | Senha    |
| ----------- |---------:|
| 506558920   | 1010     |
| 000100726   | 1010     |
| 448650425   | 1010     |


### Build

O processo de geração de builds ocorre através do [Fastlane](https://fastlane.tools/) e [Travis](https://travis-ci.com/).
A cada push do commit realizado entra para uma fila de geração de build. Esta fila se encontra dentro do [Travis](https://travis-ci.com/) e é possível acesso com o usuário e senha do Github da Smiles.

Há algumas flags configuradas para geração de build que são importantes ter conhecimento.

Estas flags são utilizadas junto ao commit para o Travis, onde é seguido um roteiro para geração dos builds.

* `[qa]`: Flag utilizada para gerar um build e enviar um e-mail ao QA da Smiles notificando de nova versão;
* `[testflight]`: Flag utilizada para enviar o build para o TestFlight da Apple. Este é utilizado exclusivamente quando a Smiles solicita um build de produção para testes antes de um deploy final na loja.
* `[bump]`: Flag utilizada para subir a versão do aplicativo. Normalmente é utilizada quando se gera uma versão que irá para loja, onde o número final fica sempre como 0 (zero). Ex.: `2.69.0`.

É possível também gerar uma versão a partir de um commit sem novos itens. Um exemplo baseado nisto é quando foi gerado todo ajuste possível de código, o QA da Smiles validou tudo e então é necessário gerar uma versão de produção para realizar o regressivo. 
Neste caso então é necessário realizar um commit sem itens, porém utilizando as flags de build.

Para isto, é necessário que através do Terminal entre no diretório do projeto e digite o comando abaixo:

```
git commit --allow-empty -m "Texto a ser referênciado no commit"
```
ou 
```
git commit --allow-empty -m "Gerar versão da release [bump][qa][testflight]"
```

Após isto basta realizar o `push` para o servidor e aguardar.

É possível também realizar builds locais utilizando o fastlane, porém este caso é indicado apenas se houver uma urgência na geração do build e o processo automático estiver com problemas.

* Build em branches com upload para hockey app usando schema Smiles_Homologacao
```
fastlane ios qa_homolog
```

* Build em branches com upload para hockey app usando schema Smiles_Producao
```
fastlane ios qa_prod
```

* Build em branches com upload para AppleStore app usando schema Smiles_Loja
```
fastlane ios release_testflight
```



###### Aconselhamos o uso da interface de Git como [SourceTree](https://www.sourcetreeapp.com/) para facilitar na gestão de alterações de código.
