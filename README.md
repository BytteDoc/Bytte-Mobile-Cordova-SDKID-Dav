![Directories](http://www.bytte.com.co/ftpaccess/Varios/CarlosG/Documentaci%C3%B3n/LogoBytte.png)

# Bytte SDK
# Documento Integración SDK Cordova
### CONFIDENCIALIDAD

La información contenida en el presente documento es CONFIDENCIAL, hace parte del secreto comercial e industrial de la empresa e implica transmisión de información cuya propiedad corresponde exclusivamente a BYTTE SAS. En consecuencia, la divulgación o el uso inapropiado de la información aquí contenida por parte del receptor de la misma, implicarán la aplicación de las normas legales pertinentes para su debida protección.

### 1. INTRODUCCIÓN

#### Propósito General del Documento

El presente documento tiene como finalidad dar a conocer el paso a paso de la instalación del SDK provisto por Bytte en una aplicación hibrida generada en Cordova.

#### 1.1. Objetivo

El presente documento tiene como objetivo explicar basado en un ejemplo, cómo realizar la integración del SDK Bytte a una aplicación Cordova.

#### 1.2. Factores Limitantes

Los factores limitantes para la integración del SDK son:
* El Plugin SDK Bytte, está disponible para plataformas IOS y Android únicamente.
* Se recomiendan cámaras con resolución mayores o iguales a 8 Mega Pixeles para un óptimo rendimiento.
* Se debe verificar la calidad de la cámara, es recomendable utilizar dispositivos con cámara que tengan la característica de “Auto Foco” habilitada.
* El SDK no funciona sobre dispositivos virtuales, únicamente sobre dispositivos físicos IPhone y Android.

### 2. INSTALACIÓN

#### 2.1. Pre requisitos

* General:
    > * NPM (sistema de gestión de paquetes)

* Para la compilación de aplicación en plataforma IOS, se requiere:
    > * XCode 12 o Superior con SDK IOS 12 o superior.

#### 2.2. Instalación Plugin com.bytte.sdk.biometric

NOTA: Para este ejemplo, el Plugin ubicado en la carpeta CDVBytteBioLibV3, debe estar al mismo nivel de la aplicación destino.

`$ cordova plugin add ../CDVBytteBioLibV3/`

Una vez instalado el plugin, se debe realizar la consulta a la aplicación para verificar que este quedó correctamente instalado. (`$ cordova plugin ls`)

`$ com.bytte.sdk.biometric (Version) "Bytte SDK Biometric"`

#### 2.3. Configuración nativo iOS (XCode)

Una vez adicionado el plugin, se debe realizar el proceso de preparación de la aplicación, para ello se debe ejecutar el siguiente comando:

`$ cordova prepare ios`

Se debe acceder a la carpeta ../platforms/ios/<NombreProyectoDestino>. Xcodeproj como se muestra en la imagen:

![Directories](http://www.bytte.com.co/ftpaccess/Varios/CarlosG/Cordova/plataformaIos.png)

Al acceder al proyecto, se debe seleccionar el certificado con que debe compilarse la aplicación destino.

Para el correcto funcionamiento de la aplicación, se debe deshabilitar el BitCode.

![Directories](http://www.bytte.com.co/ftpaccess/Varios/CarlosG/Documentaci%C3%B3n/Bitcode.png)

#### 2.3.1. Librerías Embebidas iOS

* La aplicación debe tener las siguientes librerías como recurso embebido en el folder “Frameworks” como lo indica la imagen:

![Directories](http://www.bytte.com.co/ftpaccess/Varios/CarlosG/Documentaci%C3%B3n/LibreriasBytteF.png)


  > * BytteLibrarySDKComun.framework
  > * BytteLibrarySDKDocumentoV2.framework
  > * BytteLibrarySDKFaceID.framework
  > * BytteLIbrarySDKFingerID.framework
  > * Identy.framework
  > * IdentyFace.framework
  > * Microblink.framework


#### 2.3.2. Archivos de licencia

Bytte proporciona los archivos de licencia requeridos para las siguientes capturas.

  > * Captura de Huellas.
  > * Captura de Selfie.
  
Se deben embeber los archivos como recursos.

![Directories](http://www.bytte.com.co/ftpaccess/Varios/CarlosG/Documentaci%C3%B3n/ArchivosLicencia.png)

Se deben tener presentes los nombres de la licencia al momento de invocar el llamado a la captura facial y dactilar.

#### 2.4. Configuración nativo Android

#### 2.5. Uso de la librería

* Una vez instalado el plugin, la aplicación destino heredará el Javascript expuesto por este, el cual expone las siguientes operaciones:
  > * startPhotoCapture
  > * startFindFile
  > * startBarCode
  > * startFrontDocument
  > * startCreditCard
  > * startFaceCapture
  > * startFingerprint

##### ***startPhotoCapture***

```javascript
//Inicia la Cámara para toma de foto
//arg0 párametro Vacío 
//arg1 párametro ancho de la imagen 
//arg2 párametro alto de la imagen 
//arg3 párametro monocromático 1 - imagen monocromático ok 0- image monocromático  fail 
exports.startPhotoCapture = function(arg0,arg1,arg2,arg3,success, error) {
    exec(success, error, "CDVBytteBioLib", "startPhotoCapture",[arg0, arg1, arg2, arg3]);
};
```

##### ***startFindFile***

```javascript
//Inicia la el buscador de archivos
//arg0 identifica el tipo de busqueda 0-> file .pdf ---1->galeria .png-.jpg
exports.startFindFile = function(arg0, success, error) {
    exec(success, error, "CDVBytteBioLib", "startFindFile",[arg0]);
};
```

##### ***startBarCode***

```javascript
//Inicia la Captura de la imagen y Código de Barras!
//arg0 Código Activación Licencia
//arg1 KeyPass
//arg2 TimeOut
exports.startBarCode = function(arg0, arg1, arg2 , success, error) {
     exec(success, error, "CDVBytteBioLib", "startBarCode", [arg0, arg1, arg2]);
};
```

##### ***startFrontDocument***

```javascript
//Inicia la Captura del Frente del Documento!
//arg0 Código Activación Licencia
//arg1 KeyPass
//arg2 TimeOut
exports.startFrontDocument = function(arg0, arg1, arg2, success, error) {
    exec(success, error, "CDVBytteBioLib", "startFrontDocument", [arg0, arg1, arg2]);
};
```

##### ***startCreditCard***

```javascript
//Inicia la Cámara para toma de tarjeta de crédito
//arg0 : Key
//arg1 : FilePwd -> Password con que se ofuscaron las imágenes
//arg2 : TimeOut
exports.startCreditCard = function(arg0, arg1, arg2,success, error) {
    exec(success, error, "CDVBytteBioLib", "startCreditCard",[arg0, arg1, arg2]);
};
```

##### ***startFaceCapture***

```javascript
//Inicia la Captura del Selfie
//arg0 KeyPass
//arg1 TimeOut
//arg2 namePath
//arg3 url
//arg4 camera
//arg5 netkey
exports.startFaceCapture = function(arg0, arg1, arg2, arg3,arg4,arg5, success, error) {
    exec(success, error, "CDVBytteBioLib", "startFaceCapture", [arg0, arg1, arg2, arg3,arg4,arg5]);
};
```

##### ***startFingerprint***

```javascript
//Inicia la Captura de la huella
//arg0 KeyPass
//arg1 TimeOut 
//arg2 Numero de Dedo (1 al 10)
//arg3 namePath
//arg4 url
//arg5 netkey
exports.startFingerprint = function(arg0, arg1, arg2, arg3,arg4,arg5, success, error) {
    exec(success, error, "CDVBytteBioLib", "startFingerprint", [arg0, arg1, arg2, arg3,arg4,arg5]);
};
```










