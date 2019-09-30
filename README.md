# CameraBio Android

Este projeto visa facilitar a implementação do frame de captura biométrica via aplicativos Android. 

## Começando

Estas instruções farão com que você consiga implementar a câmera com engenharia biométrica pré-existente e obter/manipular os dados de retorno.

### Pré requisitos

- Android Studio - IDE oficial de desenvolvimento Google. Versão 9 ou superior
- Maven Jitpack - Gerenciador de bibiotecas para a IDE.
- Precisamos também do arquivo googleservices.json referente ao seu projeto. Crie e adicione na pasta app do seu diretório. Precisa de ajuda? Segue o link: [Google Console](https://console.firebase.google.com)   

### Instalando

- Abra o arquivo build.gradle (Projeto) e adicione Jitpack manager em repositorios, seu código deve parecer com isto: 

```
allprojects {
    repositories {
        google()
        jcenter()
        maven { url 'https://jitpack.io'}
        }
}
```

- Adicione suporte ao AndroidX ao seu arquivo build.properties:
```
android.useAndroidX=true
android.enableJetifier=true
````
Se faz necessário para uma melhor performance e funcionamento do frame de captura

- Em seguida, abra o arquivo build.gradle (Modulo) e adicione nossa dependência ao seu projeto: 

```
 implementation 'com.github.acesso-io:camerabio-android:1.0.0'
```

Pronto! O seu projeto já está pronto para o uso de nossa ferramenta.

## Manuseio

Importar, inicializar e receber os callbacks básicos é muito simples, siga os passos abaixo:

- Abra a sua Activity ou Fragment que deseja manusear nossa sdk e adicione as seguintes linhas: 

```
import com.example.camerabio.CallbackBio;
import com.example.camerabio.RestBio;

public class MainActivity extends AppCompatActivity implements CallbackCameraBio {

       CameraBioManager cb = new CameraBioManager(MainActivity.this);
       cb.startCamera();

}
```

Pronto, importamos e inicializamos nossa solução... Estamos quase lá!  


Note que implementamos o CallbackCameraBio, responsável pelos retornos de nossa sdk. Ele irá indicar que implemente os seguintes métodos: 

```
 @Override
 public void onSuccessCapture(String base64) {
  // Aqui está o base64 da captura    
 }

@Override
public void onFailedCapture(String description) {
  // Algo deu errado
}
```

Tranquilo, certo? Falta apenas instanciar nossa classe RestBio e inicializar o serviço com sua instância e dados de acesso.

E Voila! Nossa solução está pronta para o uso!!! 

Simples, não? xD 

### Outros métodos uteis

Voce pode também iniciar a camera voltada para capturas de Documentos, é bem simples: 

```

  CameraBioManager cb = new CameraBioManager(MainActivity.this);
  cb.startCameraDocument(cb.RG_FRENTE);

```

Note que acima estamos inicalizando a abertura de câmera especificando o tipo de documento para máscara. 
Atualmente temos 3 tipos de documentos: 

 - cb.RG_FRENTE,
 - cb.RG_VERSO,
 - cb.CNH

Caso deseje apenas abrir a camera para capturar documento sem nenhuma mascara acima, escolha a opcao:

 - cb.NONE
 

E o retorno: 

```
 @Override
 public void onSuccessCaptureDocument(String base64) {
  // Aqui está o base64 da captura    
 }

@Override
public void onFailedCaptureDocument(String description) {
  // Algo deu errado
}
```


## Construido com

* [Retrofit](https://square.github.io/retrofit/) - Framework para suporte REST


## Versionamento

Nós usamos [Github](https://github.com/) para versionar. Para as versões disponíveis, veja as [tags do repositório](https://github.com/acesso-io/camerabio-android/releases). 

## Autores

* **Matheus Domingos** - *Engenheiro Mobile* - [GitHub](https://github.com/MatheusDomingos)

Veja também nossa lista de [contribuidores](https://github.com/acesso-io/camerabio-android/graphs/contributors) que participaram deste projeto.

## Licença

Este proje é licenciado pela MIT License - veja [LICENSE.md](LICENSE.md) o arquivo para detalhes


