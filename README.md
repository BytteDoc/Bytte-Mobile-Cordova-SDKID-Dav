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

#### 2.2.1 Configuración archivo .npmrc

Una vez instalado NPM (sistema de gestión de paquetes). En la ruta por defecto de instalación se debe encontrar el archivo .npmrc, si no se encuentra se debe crear a nivel de usuario.

Una vez detectado el archivo se debe configurar de la siguiente manera.


``` txt

registry=https://byttetfs.pkgs.visualstudio.com/c1dcbe70-4508-4f44-bfa8-e50bdbfea41f/_packaging/Bytte-Library-Sdk-Cordova-Dav/npm/registry/ 
                        
always-auth=true

; begin auth token
//byttetfs.pkgs.visualstudio.com/c1dcbe70-4508-4f44-bfa8-e50bdbfea41f/_packaging/Bytte-Library-Sdk-Cordova-Dav/npm/registry/:username=BytteTFS
//byttetfs.pkgs.visualstudio.com/c1dcbe70-4508-4f44-bfa8-e50bdbfea41f/_packaging/Bytte-Library-Sdk-Cordova-Dav/npm/registry/:_password=(TOKEN)
//byttetfs.pkgs.visualstudio.com/c1dcbe70-4508-4f44-bfa8-e50bdbfea41f/_packaging/Bytte-Library-Sdk-Cordova-Dav/npm/registry/:email=npm requires email to be set but doesn't use the value
//byttetfs.pkgs.visualstudio.com/c1dcbe70-4508-4f44-bfa8-e50bdbfea41f/_packaging/Bytte-Library-Sdk-Cordova-Dav/npm/:username=BytteTFS
//byttetfs.pkgs.visualstudio.com/c1dcbe70-4508-4f44-bfa8-e50bdbfea41f/_packaging/Bytte-Library-Sdk-Cordova-Dav/npm/:_password=(TOKEN)
//byttetfs.pkgs.visualstudio.com/c1dcbe70-4508-4f44-bfa8-e50bdbfea41f/_packaging/Bytte-Library-Sdk-Cordova-Dav/npm/:email=npm requires email to be set but doesn't use the value
; end auth token
```

En el espacio (*TOKEN*) se debe ingresar el password enviado por Bytte sas.

#### 2.2.2 Instalación 

`$ cordova plugin add com.bytte.sdk.biometric --save`

![Directories](http://www.bytte.com.co/ftpaccess/Varios/CarlosG/Cordova/npm.png)

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

se deben tener presentes los nombres de la licencia al momento de invocar el llamado a la captura facial y dactilar.

# 2.4. Configuración  Android

## Captura de Insumos 
El app debe solicitar los permisos  en tiempo de ejecución antes de usar la funcionalidad y validar que el permiso fue otorgado

### Verificamos la configuracion cordova para android y adicionamos el plugin que se les entrega.
### tomar el path del plugin descargado
``` terminal 
cordova platform add android
cordova plugin add com.bytte.sdk.biometric --save
```

#### Para la configuración de Android ahora se maneja por maven para el uso de estas dependencias debemos tener en cuenta lo siguiente: confirmar los datos de username y token. Para solicitarlos a bytte antes de su desarrollo. Estos nos dan el acceso a las dependencias necesarias de las capturás de huellas, documento colombiano de hologramas


### soporte a arquitecturas arm 32 y 64 bits 
``` gradle


android{ 
    defaultconfig  despues de 
    versionName ingresamos 
    ndk {abiFilters  “armeabi-v7a”, "arm64-v8a"}


  maven {
         url 'https://multifactorbyttelibrary.pkgs.visualstudio.com/BytteSDKLibraryX/_packaging/SDKBytteV2/maven/v1'
         name 'SDKBytteV2'
        credentials {
            username ""
            password ""
        }
    }
```

## licencias Documentos 
> * Identificador de la aplicacion 'packagename' ejm: *com.biometric.bytte.casbauth
> * Se esntrega una cadena con el siguiente formato:
> * sRwAAAAYY29tLmxvc2FuZGVzcHJlcGFnby50YXBw65mSy/13Bcc1rGbVKla2wsuEGRZ8bunSfSt8+JnzW+QzG2aIrzOH+kk1UixKehUiOG62x8FNjIF1CcbKM4aLgHHdOLni7+UMfDpYe+pky26XC/YxvnD5cYCQ2dI4RhqJHKSZiLH6fwLfZXVPnF3wgGyZMRrmOW/yu0V0wLaOEpC8rJaDxIwQvwTOm0/BL5/Y901Z+dALX1U/6KmeP+deJy1oshQ85A4IgH4uNmSStQAnor4=
Esta licencia es necesaria para el uso del sdk y captura de documentos.


# licencias Biometria

### Parametros


**Se entrega un archivo y este se ingresara en el directorio: android/app/src/assets**
<p align="center" >
  <img src="src/assets.png"  width="400" height="400">
</p>

## licencia  Android para el uso de huellas
* **crear una carpeta en el direccorio android llamada assets**
Dentro de esa carpeta depositamos el archivo de licencia que se generara para la implementación en debug y otra para reléase
* **estas licencias estan vinculadas al sha1 del keystore de la app tanto para  produccion como para desarrollo. Como tan bien al namepackage de la app**

para validar que sha1 tienes como desarrollo usa la la siguiente linea en una terminal. (valida el  path y la demas info para aplicar en cada caso)
```
keytool -list -v -keystore ~/.Android/debug.keystore -alias androiddebugkey -storepass Android -keypass Android 
```

## configuracion colores de la pantalla de huellas
```    

>boxes -> color de borde  del cuadro de la camara
>boxes_transparent -> color del recuadro  entre el header y el footer
>colorPrimary -> color del footer y el header 

    ```  xml
    <color name="boxes">#FF5722</color>
    <color name="boxes_transparent">#FF5722</color>
    <color name="colorPrimary">#FFC107</color>
    <color name="colorPrimaryDark">#FF5722</color>

    ```
## configuracion en español para mensajes  huellas
vamos a la carpeta res/values/strings.xml

``` xml
 <string name="id_searching_left">Buscando dedos izquierdos…</string>
    <string name="id_searching_right">Buscando dedos derechos…</string>




        <string name="id_authentication_retake">INSEGURO VOLVER A TOMAR</string>
        <string name="id_authentication_successful">Autenticado</string>
        <string name="id_authentication_unsuccessful">Autenticación incorrecta</string>
        <string name="id_capture_completed">Captura completada</string>
        <string name="id_captured">Capturado</string>
        <string name="id_capturing">Capturando..</string>
        <string name="id_close">Cerrar</string>
        <string name="id_confirm_exit">Confirmar salida</string>
        <string name="id_continue">SEGUIR</string>
        <string name="id_dshow_again">No me lo muestres de nuevo</string>
        <string name="id_enrollment_completed">INSCRIPCIÓN FINALIZADA</string>
        <string name="id_exit_text">¿Quieres salir de Capture?</string>
        <string name="id_good_quality">Todo de buena calidad</string>
        <string name="id_hand_closer">Por favor acerca la mano</string>
        <string name="id_hand_further_away">Mueva la mano más lejos</string>
        <string name="id_hand_further_away_ff">Mueva la mano más lejos 4F</string>
        <string name="id_hold_0">Por favor sostenga</string>
        <string name="id_hold_1">Por favor sostenga 1</string>
        <string name="id_hold_2">Por favor sostenga 2</string>
        <string name="id_hold_3">Por favor sostenga 3</string>
        <string name="id_hold_4">Por favor sostenga 4</string>
        <string name="id_hold_5">Por favor sostenga 5</string>
        <string name="id_hold_6">Por favor sostenga 6</string>
        <string name="id_hold_still">Asegúrate de mantenerte quieto hasta la captura automática. </string>
        <string name="id_identy_template_format">Formato de plantilla IDENTY</string>
        <string name="id_image_cd_todo">QUE HACER</string>
        <string name="id_in_front_camera">2.Coloque los dedos frente a la cámara</string>
        <string name="id_index">ÍNDICE    </string>
        <string name="id_index_finger">dedo índice</string>
        <string name="id_inside_guide">Por favor, esté dentro de la guía.</string>
        <string name="id_keep_fingers">1.Extiende y mantén los dedos juntos</string>
        <string name="id_keep_fingers_together">mantener los dedos juntos</string>
        <string name="id_left_thumb"> PULGAR IZQUIERDO</string>
        <string name="id_little">PEQUEÑO   </string>
        <string name="id_little_finger">dedo índice</string>
        <string name="id_location_error_off">Algo es extraño APAGADO</string>
        <string name="id_middle">MEDIO   </string>
        <string name="id_middle_finger">dedo medio</string>
        <string name="id_next">SIGUIENTE</string>
        <string name="id_next_detection">Pasar a la siguiente mano ?</string>
        <string name="id_next_hand_confirm">Siguiente detección Confirmar</string>
        <string name="id_no">NO</string>
        <string name="id_no_match">SIN COINCIDENCIA</string>
        <string name="id_not_good_quality">no tiene buena calidad.</string>
        <string name="id_ok">OK</string>
        <string name="id_pic_qc_title">FALLO EN LA CALIDAD DE LA IMAGEN</string>
        <string name="id_processing">Procesando …</string>
        <string name="id_qc_retake">Necesitamos retomar la foto</string>
        <string name="id_quality_failed">Falló la calidad de la imagen</string>
        <string name="id_retake_additional_tip">Consejos adicionales</string>
        <string name="id_retake_match">Se alcanzó el número máximo de intentos, inténtelo de nuevo</string>
        <string name="id_retake_q">volver a tomar?</string>
        <string name="id_retake_string">volver a tomar</string>
        <string name="id_retake_tip_1">Tus dedos miran hacia la cámara</string>
        <string name="id_retake_tip_2">Tus dedos están dentro de la caja azul</string>
        <string name="id_retake_tip_3">Utilice iluminación interior normal</string>
        <string name="id_retry">Procesar de nuevo</string>
        <string name="id_right_thumb">PULGAR DERECHO</string>
        <string name="id_ring">ANILLO     </string>
        <string name="id_ring_finger">dedo anular</string>
        <string name="id_select_hand">por favor seleccione al menos una mano</string>
        <string name="id_spoof">PARODIA</string>
        <string name="id_spoof_additional_tip">Consejos adicionales</string>
        <string name="id_spoof_question">¿Estás usando manos reales para autenticarte?</string>
        <string name="id_spoof_tip_2">Utilice iluminación interior normal  </string>
        <string name="id_spoof_tip_3">Intente intentar una ubicación / fondo diferente</string>
        <string name="id_spoof_title">Spoof detectado</string>
        <string name="id_stable">Por favor sea estable</string>
        <string name="id_stay_still_blue">3.Quédate quieto dentro del rectángulo azul</string>
        <string name="id_success">Éxito</string>
        <string name="id_success_match"> MATCH EXITOSO</string>
        <string name="id_thumb">PULGAR    </string>
        <string name="id_thumb_finger">dedo índice</string>
        <string name="id_try_again">Intentar otra vez</string>
        <string name="id_try_again_in">Inténtelo de nuevo en : </string>
        <string name="id_wait_auto">4.Espere la captura automática (hasta que se apague el flash)</string>
        <string name="id_wsq_compression">Relación de compresión WSQ</string>
        <string name="id_yes">SI</string>
        <string name="id_zero">0</string>
```


## configuracion colores de la pantalla de facial
### Colores para personalizar la vista 
Estos colores se toman de la configuracon de la app 
>id_box -> color del mensaje 
>id_face_boxes -> color del del borde
>colorPrimary -> color del footer y el header 
```
  
    <color name="id_box">#FF5722</color>
    <color name="id_face_boxes">#8BC34A</color>
```



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
    exec(success, error, "BytteBioLib", "startPhotoCapture",[arg0, arg1, arg2, arg3]);
};
```

##### ***startFindFile***

```javascript
//Inicia la el buscador de archivos
//arg0 identifica el tipo de busqueda 0-> file .pdf ---1->galeria .png-.jpg
exports.startFindFile = function(arg0, success, error) {
    exec(success, error, "BytteBioLib", "startFindFile",[arg0]);
};
```

##### ***startBarCode***

```javascript
//Inicia la Captura de la imagen y Código de Barras!
//arg0 Código Activación Licencia
//arg1 KeyPass
//arg2 TimeOut
exports.startBarCode = function(arg0, arg1, arg2 , success, error) {
     exec(success, error, "BytteBioLib", "startBarCode", [arg0, arg1, arg2]);
};
```

##### ***startFrontDocument***

```javascript
//Inicia la Captura del Frente del Documento!
//arg0 Código Activación Licencia
//arg1 KeyPass
//arg2 TimeOut
exports.startFrontDocument = function(arg0, arg1, arg2, success, error) {
    exec(success, error, "BytteBioLib", "startFrontDocument", [arg0, arg1, arg2]);
};
```

##### ***startCreditCard***

```javascript
//Inicia la Cámara para toma de tarjeta de crédito
//arg0 : Key
//arg1 : FilePwd -> Password con que se ofuscaron las imágenes
//arg2 : TimeOut
exports.startCreditCard = function(arg0, arg1, arg2,success, error) {
    exec(success, error, "BytteBioLib", "startCreditCard",[arg0, arg1, arg2]);
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
    exec(success, error, "BytteBioLib", "startFaceCapture", [arg0, arg1, arg2, arg3,arg4,arg5]);
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
exports.startFingerprint = function(arg0, arg1, arg2, arg3,arg4, success, error) {
    exec(success, error, "BytteBioLib", "startFingerprint", [arg0, arg1, arg2, arg3,arg4]);
};
```
## Respuesta de las capturas
### Captura Back documento colombiano de hologramas 
  * BarcodeBase64
    : Código de barras en base64 que se requiere para procesos posteriores
```
{
   "BarcodeBase64":"MDMxMzUxNjkyMAAAAAAAAAAAAAAAAAAAUHViRFNLXzEAA",
   "CiudadExpedicion":"BOGOTA",
   "CiudadNacimiento":"BOGOTA DC K",
   "CodigoOperacion":"0000",
   "DepartamentoCol":"CUNDINAMARCA",
   "FechaExp":"29 MAY 2009",
   "FechaNacimiento":"1991/05/27",
   "MensajeOriginal":"Captura exitosa",
   "MensajeRetorno":"Ok Captura",
   "NombresCompletos":"XXXXXX ",
   "NumeroCedula":"1069258777",
   "NumeroTarjeta":"1235889",
   "Pais":"COLOMBIA",
   "PathImagen":"/data/user/0/com.davivienda.nuevaappemp/files/Documents/DB_IMG_175dcec7_9313_48bb_aa89_9c34406707b0.jpg",
   "PrimerApellido":"XXXX",
   "PrimerNombre":"XXXX",
   "RH":"O+",
   "SegundoApellido":"XXX",
   "SegundoNombre":"XXXX",
   "Sexo":"M",
   "StatusOperacion":true,
   "TipoDedo":"2",
   "TipoDedo2":"7",
   "VersionCedula":"03"
}
```

### Captura Frente documento colombiano de hologramas 
```
 {"CodigoOperacion":"0000",
   "MensajeOriginal":"Captura exitosa",
   "MensajeRetorno":"Ok Captura",
   "PathImagen":"/data/user/0/com.davivienda.nuevaappemp/files/Docu…s/DF_IMG_6a6124c9_deb7_42ed_9d2a_6eb4899d28ce.jpg",
   "PathImagenRostro":"/data/user/0/com.davivienda.nuevaappemp/files/Docu…s/DF_IMG_a9784878_ba42_49f0_afd6_09735dcaa732.jpg",
   "StatusOperacion":true}
```
### Captura de huellas
*	TipoDedo (Dedo impreso en el documento) principal TipoDedo
        Se define de la siguiente manera:
    > *	1 – Derecho Pulgar
    > *	2 – Derecho Índice
    > *	3 – Derecho Medio
    > *	4 – Derecho Anular
    > *	5 – Derecho Meñique
    > *	6 – Izquierdo Pulgar
    > *	7 – Izquierdo Índice
    > *	8 – Izquierdo Medio
    > *	9 – Izquierdo Anular
    > *	10 – Izquierdo Meñique
    > *	20- mano derecha
    > *	21-mano izquierda

* se retorna el  path de las img para cada una de las capturas
```
{
    "CodigoOperacion": "0000",
    "MensajeOriginal": "Captura Exitosa",
    "MensajeRetorno": "Ok Captura",
    "StatusOperacion": true,
    "FingerprintsObjects": [
        {
            "Fingerprint": "20",
            "Minutia": "",
            "PathBitmap": "/data/user/0/com.davivienda.nuevaappemp/files/Documents/FP_IMG_ecc33475_fb40_4705_9fd5_4dcdd601ec8c.jpg"
        },
        {
            "Fingerprint": "3",
            "Minutia": "",
            "PathBitmap": "/data/user/0/com.davivienda.nuevaappemp/files/Documents/FP_IMG_b3ad988f_f394_4d17_9103_71fa262316ef.jpg"
        },
        {
            "Fingerprint": "4",
            "Minutia": "",
            "PathBitmap": "/data/user/0/com.davivienda.nuevaappemp/files/Documents/FP_IMG_4e21f108_b2b4_4d2d_9fb1_daa07bff0d43.jpg"
        },
        {
            "Fingerprint": "2",
            "Minutia": "",
            "PathBitmap": "/data/user/0/com.davivienda.nuevaappemp/files/Documents/FP_IMG_2a15be0b_61f0_4e81_afd8_0d2db4801300.jpg"
        },
        {
            "Fingerprint": "5",
            "Minutia": "",
            "PathBitmap": "/data/user/0/com.davivienda.nuevaappemp/files/Documents/FP_IMG_948a03e3_2833_4701_a389_70282686a1b4.jpg"
        }
    ],
    "plataforma": "Android"
}
```
```
<string name="OK">0000</string><string name="TimeOut">0001</string>
<string name="Cancelado_a_proposito">0002</string>
<string name="Error_de_Licencia_MicroBlink">0111</string>
<string name="Error_No_tiene_permisos_camara">0112</string>
<string name="Error_de_Licencia_Biometria">0113</string>
<string name="Error_Captura_de_huellas">0114</string>


<string name="timeOut">TimeOut</string>
<string name="Canceladoproposito">Cancelado a proposito</string>
<string name="ErrorLicencia_MicroBlink">Error de Licencia MicroBlink"</string>
<string name="ErrorLicencia_Biometria">Error de Licencia biometria"</string>
<string name="Error_Capturahuellas">Error en la captura de las huellas"</string>
<string name="ErrorLicenciaBiometria">Error licencia de  biometria"</string>
```
------------------------------
Control de cambios
------------------------------
------------------------------
| 9-nov-2021 | Actualizacion librerias microblink para captura de documentos, cambio de librerias para la captura biometria|

| 12-Ene-2023| Se remueve la configuración par la solicitud de safetynet en la implementación de huellas solo afecta a android|


