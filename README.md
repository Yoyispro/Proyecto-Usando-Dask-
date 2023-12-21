# Proyecto-Usando-Dask-
# Enalce al colab 
[Proyecto dask](https://colab.research.google.com/drive/1ahX_1IP5hxL3qrmds9B_0I8W3Tq9mAcC?usp=sharing)


Mediante el uso de la biblioteca dask y dask_ml vamos a hacer el proceso de clasificación, el objetivo es predecir la probabilidad de que una máquina con Windows se infecte con varias familias de malware, en función de las diferentes propiedades de esa máquina.

Los datos de telemetría que contienen estas propiedades y las infecciones de la máquina se generaron mediante la combinación de informes de latidos y amenazas recopilados por la solución de protección de punto final de Microsoft, Windows Defender.

Cada fila en este conjunto de datos corresponde a una máquina, identificada de forma única por un MachineIdentifier. HasDetections es la verdad básica e indica que se detectó Malware en la máquina. Usando la información y las etiquetas en train.csv, debe predecir el valor de HasDetections para cada máquina en test.csv.

La detección de malware es inherentemente un problema de serie temporal, pero se complica por la introducción de nuevas máquinas, máquinas que se conectan y desconectan, máquinas que reciben parches, máquinas que reciben nuevos sistemas operativos, etc. Si bien el conjunto de datos proporcionado aquí ha sido divididos aproximadamente por tiempo, las complicaciones y los requisitos de muestreo mencionados anteriormente pueden significar que puede ver un acuerdo imperfecto entre sus puntajes de validación cruzada, públicos y privados. Además, este conjunto de datos no es representativo de las máquinas de los clientes de Microsoft en la naturaleza; se ha muestreado para incluir una proporción mucho mayor de máquinas de malware.

Columnas
Los nombres de columnas no disponibles o autodocumentados están marcados con "NA".

MachineIdentifier - ID de máquina individual

ProductName: información del estado del defensor, p. win8defensor

EngineVersion: información del estado del defensor, p. 1.1.12603.0

AppVersion: información del estado del defensor, p. 4.9.10586.0

AvSigVersion: información del estado del defensor, p. 1.217.1014.0

IsBeta: información del estado del defensor, p. FALSO

RtpStateBitfield - NA

IsSxsPassiveMode - NA

DefaultBrowsersIdentifier: ID del navegador predeterminado de la máquina

AVProductStatesIdentifier: ID para la configuración específica del software antivirus de un usuario

AVProductsInstalado - NA

AVProductsEnabled - NA

HasTpm: verdadero si la máquina tiene tpm

CountryIdentifier: ID del país en el que se encuentra la máquina

CityIdentifier: ID de la ciudad en la que se encuentra la máquina

OrganizationIdentifier: ID de la organización a la que pertenece la máquina; el ID de la organización se asigna tanto a empresas específicas como a industrias amplias

GeoNameIdentifier: ID de la región geográfica en la que se encuentra una máquina

LocaleEnglishNameIdentifier: nombre en inglés del ID de configuración regional del usuario actual

Platform: calcula el nombre de la plataforma (de las propiedades relacionadas con el sistema operativo y la propiedad del procesador)

Processor: esta es la arquitectura de proceso del sistema operativo instalado

OsVer - Versión del sistema operativo actual

OsBuild - Compilación del sistema operativo actual

OsSuite: máscara de conjunto de productos para el sistema operativo actual.

OsPlatformSubRelease: devuelve la versión secundaria de la plataforma del sistema operativo (Windows Vista, Windows 7, Windows 8, TH1, TH2)

OsBuildLab: laboratorio de compilación que generó el sistema operativo actual. Ejemplo: 9600.17630.amd64fre.winblue_r7.150109-2022

SkuEdition: el objetivo de esta función es utilizar el tipo de producto definido en MSDN para asignar un nombre de 'SKU-Edition' que sea útil en los informes de población. El tipo de producto válido se define en %sdxroot%\data\windowseditions.xml. Esta API se ha utilizado desde Vista y Server 2008, por lo que hay muchos tipos de productos que no se aplican a Windows 10. La 'Edición SKU' es un valor de cadena que se encuentra en una de tres clases de resultados. El diseño debe entregarlo cada clase.

IsProtected: este es un campo calculado derivado del campo Productos antivirus del informe Spynet. Devoluciones: A. VERDADERO si hay al menos un producto antivirus activo y actualizado ejecutándose en esta máquina. b. FALSO si no hay ningún producto AV activo en esta máquina, o si el AV está activo, pero no recibe las últimas actualizaciones. C. nulo si no hay productos antivirus en el informe. Devuelve: si una máquina está protegida.

AutoSampleOptIn: este es el valor de SubmitSamplesConsent pasado desde el servicio, disponible en CAMP 9+

PuaMode - Modo Pua habilitado desde el servicio

SMode: este campo se establece en verdadero cuando se sabe que el dispositivo está en "Modo S", como en el modo S de Windows 10, donde solo se pueden instalar las aplicaciones de Microsoft Store.

IeVerIdentifier - NA

SmartScreen: este es el valor de cadena habilitado para SmartScreen del registro. Esto se obtiene comprobando en orden, HKLM\SOFTWARE\Policies\Microsoft\Windows\System\SmartScreenEnabled y HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\SmartScreenEnabled. Si el valor existe pero está en blanco, el valor "ExistsNotSet" se envía en telemetría.

Firewall: este atributo es verdadero (1) para Windows 8.1 y superior si el cortafuegos de Windows está habilitado, según lo informado por el servicio.

UacLuaenable: este atributo informa si el tipo de usuario "administrador en modo de aprobación de administrador" está deshabilitado o habilitado en UAC. El valor informado se obtiene al leer la clave de registro HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\EnableLUA.

Census_MDC2FormFactor: una agrupación basada en una combinación de características de hardware de nivel de censo de dispositivos. La lógica utilizada para definir el factor de forma se basa en los estándares comerciales y de la industria y se alinea con la forma en que las personas piensan acerca de su dispositivo. (Ejemplos: Smartphone, Tableta pequeña, All in One, Convertible…)

Census_DeviceFamily: también conocido como DeviceClass. Indica el tipo de dispositivo para el que está destinada una edición del sistema operativo. Valores de ejemplo: Windows.Desktop, Windows.Mobile e iOS.Phone

Census_OEMNameIdentifier - NA

Census_OEMModelIdentifier - NA

Census_ProcessorCoreCount: número de núcleos lógicos en el procesador

Census_ProcessorManufacturerIdentifier - NA

Census_ProcessorModelIdentifier - NA

Census_ProcessorClass: una clasificación de procesadores en alta/media/baja. Inicialmente utilizado para SKU de nivel de precios. Ya no se mantiene ni actualiza

Census_PrimaryDiskTotalCapacity: cantidad de espacio en disco en el disco principal de la máquina en MB

Census_PrimaryDiskTypeName: nombre descriptivo del tipo de disco principal: HDD o SSD

Census_SystemVolumeTotalCapacity: el tamaño de la partición en la que está instalado el volumen del sistema en MB

Census_HasOpticalDiskDrive: verdadero indica que la máquina tiene una unidad de disco óptico (CD/DVD)

Census_TotalPhysicalRAM: recupera la RAM física en MB

Census_ChassisTypeName: recupera una representación numérica del tipo de chasis que tiene la máquina. Un valor de 0 significa xx

Census_InternalPrimaryDiagonalDisplaySizeInInches: recupera la longitud diagonal física en pulgadas de la pantalla principal

Census_InternalPrimaryDisplayResolutionHorizontal: recupera la cantidad de píxeles en la dirección horizontal de la pantalla interna.

Census_InternalPrimaryDisplayResolutionVertical: recupera la cantidad de píxeles en la dirección vertical de la pantalla interna

Census_PowerPlatformRoleName: indica el perfil de administración de energía preferido por el OEM. Este valor ayuda a identificar el factor de forma básico del dispositivo.

Census_InternalBatteryType - NA

Census_InternalBatteryNumberOfCharges - NA

Census_OSVersion: ejemplo de versión de sistema operativo numérico: 10.0.10130.0

Census_OSArchitecture: arquitectura en la que se basa el sistema operativo. Derivado de OSVersionFull. Ejemplo - amd64

Census_OSBranch: rama del sistema operativo extraída de OsVersionFull. Ejemplo: OsBranch = fbl_partner_eeap donde OsVersion = 6.4.9813.0.amd64fre.fbl_partner_eeap.140810-0005

Census_OSBuildNumber: número de compilación del sistema operativo extraído de *OsVersionFull. Ejemplo: OsBuildNumber = 10512 o 10240

Census_OSBuildRevision: revisión de compilación del sistema operativo extraída de OsVersionFull. Ejemplo: OsBuildRevision = 1000 o 16458

Census_OSEdition: edición del sistema operativo actual. Procedente de HKLM\Software\Microsoft\Windows NT\CurrentVersion@EditionID en el registro. Ejemplo: Empresa

Census_OSSkuName: nombre descriptivo de la edición del SO (actualmente solo Windows)

Census_OSInstallTypeName: descripción amigable de qué instalación se usó en la máquina, es decir, limpia

Census_OSInstallLanguageIdentifier - NA

Census_OSUILocaleIdentifier - NA

Census_OSWUAutoUpdateOptionsName: nombre descriptivo de la configuración de actualización automática de WindowsUpdate en la máquina.

Census_IsPortableOperatingSystem: indica si el sistema operativo se inicia y se ejecuta a través de Windows-To-Go en una memoria USB.

Census_GenuineStateName: nombre descriptivo de OSGenuineStateID. 0 = Genuino

Census_ActivationChannel: clave de licencia minorista o clave de licencia por volumen para una máquina.

Census_IsFlightingInternal - NA

Census_IsFlightsDisabled: indica si la máquina participa en la distribución de tramos.

Census_FlightRing: el anillo para el que el usuario del dispositivo desea recibir vuelos. Esto podría ser diferente del anillo del sistema operativo que está instalado actualmente si el usuario cambia el anillo después de obtener un vuelo de un anillo diferente.

Census_ThresholdOptIn - NA

Census_FirmwareManufacturerIdentifier - NA

Census_FirmwareVersionIdentifier - NA

Census_IsSecureBootEnabled: indica si el modo de inicio seguro está habilitado.

Census_IsWIMBootEnabled - NA

Census_IsVirtualDevice: identifica una máquina virtual (modelo de aprendizaje automático)

Census_IsTouchEnabled: ¿es este un dispositivo táctil?

Census_IsPenCapable: ¿el dispositivo admite entrada de lápiz?

Census_IsAlwaysOnAlwaysConnectedCapable: recupera información sobre si la batería permite que el dispositivo esté siempre conectado.

Wdft_IsGamer: indica si el dispositivo es un dispositivo de jugador o no en función de su combinación de hardware.

Wdft_RegionIdentifier - NA

Tareas
Lo interesante de éste conjunto de datos es que contiene un npumero grande de registros y que nos permite realizar muchas tareas de preprocesamiento. Así que para ello sigan nuestro proceso de siempre:

Cargar el conjunto de datos
Inspeccionar los atributos y su distribución (desde éste punto se puede analizar si alguna columna tiene la mayoría o todos los registres con valores faltantes)
Separar los valores de clases de los atributos
Hacer la limpieza de nuestros datos
Generar los conjuntos de entrenamiento de los de prueba
Definir un método de clasificación y sus hiperparámetros
Hacer el entrenamiento (ajuste) de los modelos
Realizar predicciones en el conjunto de prueba
Evaluar el rendimiento
Para éste conjunto de datos observen lo siguiente, ya tenemos un archivo que dice test y uno que dice train, es decir, ya vienen las particiones de del conjunto de entrenamiento y de prueba. Aunque eso podría indicar que ya no tenemos que realizar entonces el paso 5, si tenemos que tomar en consideración que cualquier preprocesamiento que hagamos se tiene que hacer en los datos de ambos archivos.

Como siempre observen qué datos pueden descartar, ya sea por valores faltantes o por alta colinealidad (información redundante), para simplificar el proceso, también pueden eliminar registros que tengan muchos valores faltantes (aunque sabemos que eso no se hace así tan arbitrariamente en ámbito laboral).

Observen el comportamiento de los datos restantes en cuanto a su distribución (histogramas) o su relación (dispersión). Todo eso además de que sirve para generar reportes es para darnos una idea de qué atributos son relevantes para el problema y cuáles no lo son o son repetitivos.

Finalmente, espero que prueben con al menos tres métodos de clasificación una vez que ya tienen los datos preprocesados, los hiperparámetros déjenlos en los que vienen por default para no complicarnos, posteriormente evaluen los resultados con una matriz de confusion y con el reporte de clasificación visto.

Un último punto es que no olviden que es dask, no pierdan de vista el método compute y que cuando entrenen, lo hagan con joblib para paralelizar.
