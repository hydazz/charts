# Paperless-ngx

<img src="https://raw.githubusercontent.com/paperless-ngx/paperless-ngx/b948750/src-ui/src/assets/logo-notext.svg" align="right" width="92" alt="paperless-ngx logo">

![Version: 0.2.3](https://img.shields.io/badge/Version-0.2.3-informational?style=flat)
![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat)
![AppVersion: 2.15.1](https://img.shields.io/badge/AppVersion-2.15.1-informational?style=flat)

A community-supported supercharged version of paperless: scan, index and archive all your physical documents

**Homepage:** <https://charts.hydaz.com/charts/paperless-ngx/>

**This chart is not maintained by the upstream project and any issues with the chart should be raised
[here](https://github.com/hydazz/charts/issues/new?assignees=hydazz&labels=bug&template=bug_report.yaml&name=paperless-ngx&version=0.2.3)**

## Source Code

* <https://github.com/paperless-ngx/paperless-ngx>

## Requirements

Kubernetes: `>=1.22.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| <https://bjw-s.github.io/helm-charts> | common | 1.5.1 |
| <https://charts.bitnami.com/bitnami> | redis | 20.7.0 |
| <https://charts.hydaz.com> | paperless-ai | 0.1.3 |

## Installing the Chart

To install the chart with the release name `paperless-ngx`

### OCI (Recommended)

```console
helm install paperless-ngx oci://ghcr.io/hydazz/charts/paperless-ngx
```

### Traditional

```console
helm repo add hydaz https://charts.hydaz.com
helm repo update
helm install paperless-ngx hydaz/paperless-ngx
```

## Uninstalling the Chart

To uninstall the `paperless-ngx` deployment

```console
helm uninstall paperless-ngx
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/bjw-s/helm-charts/tree/a081de5/charts/library/common/values.yaml) from the [bjw-s common library](https://github.com/bjw-s/helm-charts/tree/a081de5/charts/library/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install paperless-ngx \
  --set env.TZ="America/New York" \
    hydaz/paperless-ngx
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install paperless-ngx hydaz/paperless-ngx -f values.yaml
```

## Custom configuration

## Values

**Important**: When deploying an application Helm chart you can add more values from the bjw-s common library chart [here](https://github.com/bjw-s/helm-charts/tree/a081de5/charts/library/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| gotenberg.enabled | bool | `true` | Enable Gotenberg sidecar |
| gotenberg.image.pullPolicy | string | `"Always"` | Gotenberg image pull policy |
| gotenberg.image.repository | string | `"gotenberg/gotenberg"` | Gotenberg image repository |
| gotenberg.image.tag | float | `8.19` | Gotenberg image tag |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"ghcr.io/paperless-ngx/paperless-ngx"` | Image repository |
| image.tag | string | `"2.15.1"` | Image tag |
| ingress.main | object | See [values.yaml](./values.yaml) | Enable and configure ingress settings for the chart under this key. |
| paperless | object | See [values.yaml](./values.yaml) | Paperless configuration [[ref]](https://docs.paperless-ngx.com/configuration/) |
| paperless-ai | object | See [values.yaml](./values.yaml) | Enable and configure paperless-ai subchart under this key.    [[ref]](https://github.com/hydazz/charts/tree/main/charts/paperless-ai) |
| paperless.address | string | "0.0.0.0" | The address Paperless should bind to |
| paperless.appLogo | string | "" | Path to an image file in the `/media/logo` directory, must include 'logo', e.g. `/logo/Atari_logo.svg` |
| paperless.appTitle | string | "" | If set, overrides the default name "Paperless-ngx" |
| paperless.apps | string | "" | A comma-separated list of Django apps to be included in Django's INSTALLED_APPS [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_APPS) |
| paperless.auth | object | `{"adminMail":"","adminPassword":"","adminUser":"","allowSignups":"","autoLoginUsername":"","defaultHTTPProtocol":"https","disableRegularLogin":false,"emailVerification":"optional","existingSecret":{"adminPasswordKey":"","adminUserKey":"","name":""},"sessionRemember":"None","social":{"accountProviders":"","allowSignups":false,"autoSignup":false,"existingSecret":""}}` | Authentication configuration |
| paperless.auth.adminMail | string | "" | Specify superuser email address. Only used when PAPERLESS_ADMIN_USER is set |
| paperless.auth.adminPassword | string | "" | Only used when PAPERLESS_ADMIN_USER is set. This will be the password of the automatically created superuser |
| paperless.auth.adminUser | string | "" | If this environment variable is specified, Paperless automatically creates a superuser with the provided username at start |
| paperless.auth.allowSignups | string | "" | Allow users to sign up for a new Paperless-ngx account |
| paperless.auth.autoLoginUsername | string | "" | Specify a username so that paperless will automatically perform login with the selected user |
| paperless.auth.defaultHTTPProtocol | string | https | The protocol used when generating URLs, e.g. login callback URLs |
| paperless.auth.disableRegularLogin | bool | false | Disables the regular frontend username / password login, i.e. once you have setup SSO |
| paperless.auth.emailVerification | string | optional | Determines whether email addresses are verified during signup (as performed by Django allauth) |
| paperless.auth.existingSecret | object | `{"adminPasswordKey":"","adminUserKey":"","name":""}` | Existing Secret settings |
| paperless.auth.existingSecret.adminPasswordKey | string | "" | Define the key within the existing Secret containing the admin password |
| paperless.auth.existingSecret.adminUserKey | string | "" | Define the key within the existing Secret containing the admin username |
| paperless.auth.existingSecret.name | string | "" | Define the name of an existing Secret containing the username and password |
| paperless.auth.sessionRemember | string | None | Controls the lifetime of the session. `None`, `False` or `True` [[ref]](https://docs.allauth.org/en/latest/account/configuration.html) |
| paperless.auth.social | object | `{"accountProviders":"","allowSignups":false,"autoSignup":false,"existingSecret":""}` | Social (Django AllAuth) Authentication Configuration |
| paperless.auth.social.accountProviders | string | "" | This variable is used to set up login and signup via social account providers which are compatible with django-allauth. [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_SOCIALACCOUNT_PROVIDERS) |
| paperless.auth.social.allowSignups | bool | false | Allow users to signup for a new Paperless-ngx account using any setup third party authentication systems |
| paperless.auth.social.autoSignup | bool | false | Attempt to sign up the user using retrieved email, username etc from the third party authentication system |
| paperless.auth.social.existingSecret | string | "" | The name of existing secret containing a `accountProviders` key to configure Django AllAuth |
| paperless.binaries | object | `{"convert":"","gs":""}` | Binaries configuration [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_CONVERT_BINARY) These define paths to external binaries if they are not in your $PATH |
| paperless.binaries.convert | string | convert | The binary name for `convert` |
| paperless.binaries.gs | string | convert | The binary name for `gs` |
| paperless.consume | object | `{"barcodeScanner":"PYZBAR","barcodes":{"ASNBarcodePrefix":"ASN","dpi":300,"enableASNBarcode":"","enableTagBarcode":false,"enabled":false,"string":"PATCHT","tagBarcodeMapping":"","tiffSupport":false,"upscale":"0.0"},"collate":{"doubleSidedSubdirName":"","doubleSidedTiffSupport":false,"enableDoubleSided":false},"dateOrder":"","deleteDuplicates":false,"filenameDateOrder":"","iNotify":{"delay":"0.5"},"ignoreDates":"","ignorePatterns":"","numberOfSuggestedDates":3,"polling":{"delay":5,"enabled":0,"retryCount":5},"postConsumeScript":"","preConsumeScript":"","recursive":false,"subdirsAsTags":false,"thumbnailFontName":""}` | Consumption configuration |
| paperless.consume.barcodeScanner | string | PYZBAR | Sets the barcode scanner used for barcode functionality |
| paperless.consume.barcodes | object | `{"ASNBarcodePrefix":"ASN","dpi":300,"enableASNBarcode":"","enableTagBarcode":false,"enabled":false,"string":"PATCHT","tagBarcodeMapping":"","tiffSupport":false,"upscale":"0.0"}` | Barcodes configuration |
| paperless.consume.barcodes.ASNBarcodePrefix | string | ASN | Defines the prefix that is used to identify a barcode as an ASN barcode |
| paperless.consume.barcodes.dpi | int | 300 | During barcode detection every page from a PDF document needs to be converted to an image |
| paperless.consume.barcodes.enableASNBarcode | string | "" | Enables the detection of barcodes in the scanned document and setting the ASN (archive serial number) if a properly formatted barcode is detected |
| paperless.consume.barcodes.enableTagBarcode | bool | false | Enables the detection of barcodes in the scanned document and assigns or creates tags if a properly formatted barcode is detected [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_CONSUMER_ENABLE_TAG_BARCODE) |
| paperless.consume.barcodes.enabled | bool | false | Enables the scanning and page separation based on detected barcodes |
| paperless.consume.barcodes.string | string | PATCHT | Defines the string to be detected as a separator barcode |
| paperless.consume.barcodes.tagBarcodeMapping | string | "" | Override the default dictionary of filter regular expression and substitute expressions [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_CONSUMER_TAG_BARCODE_MAPPING) NOTE: Built-in default is '{"TAG:(.*)": "\\g<1>"}' |
| paperless.consume.barcodes.tiffSupport | bool | false | Whether TIFF image files should be scanned for barcodes |
| paperless.consume.barcodes.upscale | string | "0.0" | Defines the upscale factor used in barcode detection |
| paperless.consume.collate | object | `{"doubleSidedSubdirName":"","doubleSidedTiffSupport":false,"enableDoubleSided":false}` | Collation configuration |
| paperless.consume.collate.doubleSidedSubdirName | string | "" | The name of the subdirectory that the collate feature expects documents to arrive |
| paperless.consume.collate.doubleSidedTiffSupport | bool | false | Whether TIFF image files should be supported when collating documents |
| paperless.consume.collate.enableDoubleSided | bool | false | Enables automatic collation of two single-sided scans into a double-sided document |
| paperless.consume.dateOrder | string | "" | Paperless will try to determine the document creation date from its contents. Specify the date format Paperless should expect to see within your documents |
| paperless.consume.deleteDuplicates | bool | false | When the consumer detects a duplicate document, it will not touch the original document |
| paperless.consume.filenameDateOrder | string | "" | Paperless will check the document text for document date information |
| paperless.consume.iNotify | object | `{"delay":"0.5"}` | iNotify configuration |
| paperless.consume.iNotify.delay | string | "0.5" | Sets the time in seconds the consumer will wait for additional events from inotify before the consumer will consider a file ready and begin consumption |
| paperless.consume.ignoreDates | string | "" | Paperless parses a document's creation date from filename and file content. You may specify a comma separated list of dates that should be ignored during this process |
| paperless.consume.ignorePatterns | string | "" | By default, paperless ignores certain files and folders in the consumption directory [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_CONSUMER_IGNORE_PATTERNS) |
| paperless.consume.numberOfSuggestedDates | int | 3 | Paperless searches an entire document for dates. The first date found will be used as the initial value for the created date [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_NUMBER_OF_SUGGESTED_DATES) |
| paperless.consume.polling | object | `{"delay":5,"enabled":0,"retryCount":5}` | Polling configuration |
| paperless.consume.polling.delay | int | 5 | If consumer polling is enabled, sets the delay in seconds between each check (above) paperless will do while waiting for a file to remain unmodified |
| paperless.consume.polling.enabled | int | 0 | If paperless won't find documents added to your consume folder, it might not be able to automatically detect filesystem changes |
| paperless.consume.polling.retryCount | int | 5 | If consumer polling is enabled, sets the maximum number of times paperless will check for a file to remain unmodified |
| paperless.consume.postConsumeScript | string | "" | After a document is consumed, Paperless can trigger an arbitrary script if you like |
| paperless.consume.preConsumeScript | string | "" | After some initial validation, Paperless can trigger an arbitrary script if you like before beginning consumption |
| paperless.consume.recursive | bool | false | Enable recursive watching of the consumption directory |
| paperless.consume.subdirsAsTags | bool | false | Set the names of subdirectories as tags for consumed files. E.g. <CONSUMPTION_DIR>/foo/bar/file.pdf will add the tags "foo" |
| paperless.consume.thumbnailFontName | string | "" | Paperless creates thumbnails for plain text files by rendering the content of the file on an image |
| paperless.conversion | object | `{"memoryLimit":"","tmpDir":""}` | Conversion configuration |
| paperless.conversion.memoryLimit | string | "" | On smaller systems, or even in the case of Very Large Documents, the consumer may explode, complaining about how it's "unable to extend pixel cache" |
| paperless.conversion.tmpDir | string | "" | Similar to the memory limit, if you've got a small system and your OS mounts /tmp as tmpfs, you should set this to a path that's on a physical disk |
| paperless.cron | object | `{"emailTask":"*/10 * * * *","emptyTrashTask":"0 1 * * *","indexTask":"0 0 * * *","sanityTask":"30 0 * *","trainTask":"5 */1 * * *"}` | Cron configuration |
| paperless.cron.emailTask | string | "*/10 * * * *" | Email fetch schedule (crontab format). Use "disable" to turn off. |
| paperless.cron.emptyTrashTask | string | "0 1 * * *" | Empty trash schedule |
| paperless.cron.indexTask | string | "0 0 * * *" | Search index update schedule. Use "disable" to turn off. |
| paperless.cron.sanityTask | string | "30 0 * *" | Sanity checker schedule. Use "disable" to turn off. |
| paperless.cron.trainTask | string | "5 */1 * * *" | Classifier training schedule. Use "disable" to turn off. |
| paperless.data | object | `{"paths":{"consumptionDir":"","dataDir":"","emailCertificateLocation":"","emptyTrashDir":"","filenameFormat":"","filenameFormatRemoveNone":false,"loggingDir":"","mediaRoot":"","modelFile":"","nltkDir":"","staticDir":"","supervisordWorkingDir":"","trashDir":""}}` | Application data (paths/filenames) configuration |
| paperless.data.paths | object | `{"consumptionDir":"","dataDir":"","emailCertificateLocation":"","emptyTrashDir":"","filenameFormat":"","filenameFormatRemoveNone":false,"loggingDir":"","mediaRoot":"","modelFile":"","nltkDir":"","staticDir":"","supervisordWorkingDir":"","trashDir":""}` | Paths configuration |
| paperless.data.paths.consumptionDir | string | "" | Define a custom consumption directory |
| paperless.data.paths.dataDir | string | "" | Define a custom data directory |
| paperless.data.paths.emailCertificateLocation | string | "" | Define a path to a certificate (chain) for TLS verification for mail servers |
| paperless.data.paths.emptyTrashDir | string | "" | Define a custom trash directory |
| paperless.data.paths.filenameFormat | string | "" | Define a custom filename format |
| paperless.data.paths.filenameFormatRemoveNone | bool | false | Omit placeholders that would resolve to 'none' in filenameFormat |
| paperless.data.paths.loggingDir | string | "" | Define a custom logging directory |
| paperless.data.paths.mediaRoot | string | "" | Define a custom media directory |
| paperless.data.paths.modelFile | string | "" | Path to store classification model (default: PAPERLESS_DATA_DIR/classification_model.pickle) |
| paperless.data.paths.nltkDir | string | "" | Define a custom NLTK processing directory |
| paperless.data.paths.staticDir | string | "" | Define a custom static directory |
| paperless.data.paths.supervisordWorkingDir | string | "" | If defined, supervisord.log and supervisord.pid will be created under the path [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_SUPERVISORD_WORKING_DIR) |
| paperless.data.paths.trashDir | string | "" | Define a custom trash directory |
| paperless.database | object | `{"certs":{"cert":"","key":"","rootCert":""},"engine":"mariadb","existingSecret":{"name":"","nameKey":"","passwordKey":"","userKey":""},"host":"","name":"paperless","password":"paperless","port":3306,"sslMode":"PREFERRED","timeout":"","user":"paperless"}` | Database configuration |
| paperless.database.certs | object | `{"cert":"","key":"","rootCert":""}` | Certificates configuration |
| paperless.database.certs.cert | string | "" | The path to a mounted TLS certificate |
| paperless.database.certs.key | string | "" | The path to a mounted TLS certificate key |
| paperless.database.certs.rootCert | string | "" | The path to a mounted TLS root certificate |
| paperless.database.engine | string | "mariadb" | Set the databaes engine (postgresql|mariadb) |
| paperless.database.existingSecret | object | `{"name":"","nameKey":"","passwordKey":"","userKey":""}` | An existing secret containing the database credentials |
| paperless.database.existingSecret.name | string | "" | Define the name of an existing Secret |
| paperless.database.existingSecret.nameKey | string | "" | Define the key within the Secret for the database name |
| paperless.database.existingSecret.passwordKey | string | "" | Define the key within the Secret for the database password |
| paperless.database.existingSecret.userKey | string | "" | Define the key within the Secret for the database user |
| paperless.database.host | string | "" | Specify a custom hostname for the database |
| paperless.database.name | string | "paperless" | The database name for the database |
| paperless.database.password | string | "paperless" | The password for the database |
| paperless.database.port | int | 5432 | The port for the database |
| paperless.database.sslMode | string | "PREFERRED" | The SSL Mode for the database |
| paperless.database.timeout | string | "" | Define a timeout for the database connection |
| paperless.database.user | string | "paperless" | The username for the database |
| paperless.emptyTrashDelay | string | 30 | Sets how long in days documents remain in the 'trash' before they are permanently deleted [[ref]](https://docs.paperless-ngx.com/configuration/#EMPTY_TRASH_DELAY) |
| paperless.enableAuditLog | bool | true | Enables the audit trail for documents, document types, correspondents, and tags |
| paperless.enableCompression | string | "1" | Enables compression of the responses from the webserver |
| paperless.enableFlower | bool | false | Enable the 'Flower' monitoring tool for 'Celery' (Paperless' task queue) [[ref]](https://flower.readthedocs.io/en/latest/index.html) |
| paperless.enableNLTK | string | "" | Enables or disables the advanced natural language processing used during automatic classification. Paperless will still perform some basic text pre-processing if disabled. |
| paperless.gid | int | 1000 | The group ID Paperless should use |
| paperless.gotenberg | object | `{"endpoint":""}` | Gotenberg configuration Ignored when when .gotenberg.enabled is true |
| paperless.gotenberg.endpoint | string | "" | Define the Apache Gotenberg endpoint |
| paperless.hosting | object | `{"HTTPRemoteUserHeaderName":"","allowedHosts":"","cookiePrefix":"","corsAllowedHosts":"","enableHTTPRemoteUser":false,"enableHTTPRemoteUserAPI":false,"forceScriptName":"","logoutRedirectURL":"","proxySSLHeader":"","staticURL":"","trustedOrigins":"","trustedProxies":"","useXForwardHost":false,"useXForwardPort":false}` | Hosting configuration |
| paperless.hosting.HTTPRemoteUserHeaderName | string | "" | Header name used to extract username for HTTP_REMOTE_USER auth [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_HTTP_REMOTE_USER_HEADER_NAME) |
| paperless.hosting.allowedHosts | string | "" | Allowed hosts for Paperless access on the internet [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_ALLOWED_HOSTS) |
| paperless.hosting.cookiePrefix | string | "" | Prefix added to cookies to identify users |
| paperless.hosting.corsAllowedHosts | string | "" | Allowed CORS hosts for API calls |
| paperless.hosting.enableHTTPRemoteUser | bool | false | Enable authentication via HTTP_REMOTE_USER (used by some SSO apps) |
| paperless.hosting.enableHTTPRemoteUserAPI | bool | false | Enable HTTP_REMOTE_USER auth directly against the API |
| paperless.hosting.forceScriptName | string | "" | Set this to /paperless if hosting under a subpath. No trailing slash. |
| paperless.hosting.logoutRedirectURL | string | "" | URL to redirect users to after logout |
| paperless.hosting.proxySSLHeader | string | "" | Set Django's SECURE_PROXY_SSL_HEADER for proxy SSL support |
| paperless.hosting.staticURL | string | "" | Static URL path override. Leave empty unless hosting under a subpath. |
| paperless.hosting.trustedOrigins | string | "" | A list of trusted origins for unsafe requests (e.g. POST). Required to access the Django admin via the web [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_CSRF_TRUSTED_ORIGINS) |
| paperless.hosting.trustedProxies | string | "" | Trusted proxy IPs, used for IP spoofing protection with tools like fail2ban |
| paperless.hosting.useXForwardHost | bool | false | Use X-Forwarded-Host header (required behind some proxies) |
| paperless.hosting.useXForwardPort | bool | false | Use X-Forwarded-Port header (required behind some proxies) |
| paperless.logging | object | `{"logrotateMaxBackups":"","logrotateMaxSize":""}` | Logging configuration |
| paperless.logging.logrotateMaxBackups | string | "" | The number of rotated log files to keep |
| paperless.logging.logrotateMaxSize | string | "" | Maximum file size for log files before they're rotated |
| paperless.maxImagePixels | string | "" | Configures the maximum size of an image PIL will allow to load without warning or error [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_MAX_IMAGE_PIXELS) |
| paperless.ocr | object | `{"additionalLanguages":"","clean":"clean","colorConversionStrategy":"","deskew":true,"imageDPI":"","language":"eng","maxImagePixels":"","mode":"skip","outputType":"pdfa","pages":"","rotatePages":true,"rotatePagesThreshold":12,"skipArchiveFile":"never","userArgs":""}` | OCR configuration [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_OCR_LANGUAGE) |
| paperless.ocr.additionalLanguages | string | "" | Additional languages for document parsing |
| paperless.ocr.clean | string | clean | Use unpaper to clean input before OCR |
| paperless.ocr.colorConversionStrategy | string | "" | Ghostscript color conversion strategy |
| paperless.ocr.deskew | bool | true | Correct skewing of input images |
| paperless.ocr.imageDPI | string | "" | DPI setting for image OCR |
| paperless.ocr.language | string | eng | Customize the language paperless uses when parsing documents |
| paperless.ocr.maxImagePixels | string | "" | Warn or block OCR for large images |
| paperless.ocr.mode | string | skip | When/how to perform OCR: `skip`, `redo`, `force` |
| paperless.ocr.outputType | string | pdfa | Type of PDF to produce |
| paperless.ocr.pages | string | "" | OCR only specified number of pages |
| paperless.ocr.rotatePages | bool | true | Correct page rotation (90°, 180°, 270°) |
| paperless.ocr.rotatePagesThreshold | int | 12 | Threshold for auto page rotation |
| paperless.ocr.skipArchiveFile | string | never | When to skip creating archived version of documents |
| paperless.ocr.userArgs | string | "" | Additional arguments to pass to OCRmyPDF |
| paperless.redis | object | `{"existingSecret":"","host":"","password":"paperless","port":6379,"prefix":"","username":""}` | Redis configuration Ignored when when .redis.enabled is true |
| paperless.redis.existingSecret | string | "" | Existing secret name containing full Redis URI in a `uri` key NOTE: Overrides all other Redis config |
| paperless.redis.host | string | "" | Redis hostname override NOTE: Defaults to a generated name like <release>-redis-master |
| paperless.redis.password | string | "paperless" | Redis password |
| paperless.redis.port | int | 6379 | Redis port |
| paperless.redis.prefix | string | "" | Redis key prefix |
| paperless.redis.username | string | "" | Redis username |
| paperless.secretKey | object | `{"existingSecret":{"key":"","name":""},"value":""}` | Secret Key settings |
| paperless.secretKey.existingSecret | object | `{"key":"","name":""}` | Existing Secret settings |
| paperless.secretKey.existingSecret.key | string | "" | Define the key within the existing Secret containing the secret key |
| paperless.secretKey.existingSecret.name | string | "" | Define the name of an existing Secret containing the secret key |
| paperless.secretKey.value | string | "" | Define a custom secret key for Paperless |
| paperless.smtp | object | `{"existingSecret":"","from":"","host":"","password":"","port":"","useSSL":false,"useTLS":false,"user":""}` | SMTP configuration [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_EMAIL_HOST) |
| paperless.smtp.existingSecret | string | "" | A secret containing `username` and `password` key SMTP authentication |
| paperless.smtp.from | string | "" | The `from` address for emails sent by Paperless |
| paperless.smtp.host | string | "" | The host to an SMTP server |
| paperless.smtp.password | string | "" | The password for an SMTP user |
| paperless.smtp.port | string | "" | The port for an SMTP server |
| paperless.smtp.useSSL | bool | false | Whether to use SSL for contacting the SMTP server |
| paperless.smtp.useTLS | bool | false | Whether to use TLS for contacting the SMTP server |
| paperless.smtp.user | string | "" | An SMTP username |
| paperless.taskWorkers | string | "" | The amount for task worker processes to spawn within the container |
| paperless.threadsPerWorker | string | "" | The amount of threads to assign each task worker process within the container |
| paperless.tika | object | `{"enabled":true,"endpoint":""}` | Tika configuration Ignored when when .tika.enabled is true |
| paperless.tika.enabled | bool | true | Enable or disable the Apache® Tika integration |
| paperless.tika.endpoint | string | "" | Define the Apache Tika endpoint |
| paperless.timeZone | string | UTC | Set the time zone here [[ref]](https://docs.paperless-ngx.com/configuration/#PAPERLESS_TIME_ZONE) |
| paperless.uid | int | 1000 | The user ID Paperless should use |
| paperless.webserverWorkers | int | 1 | The amount of Nginx worker processes to spawn for the server within the container |
| paperless.workerTimeout | string | "" | Worker timeout in seconds |
| persistence.consume | object | See [values.yaml](./values.yaml) | Configure consume volume settings for the chart under this key. |
| persistence.data | object | See [values.yaml](./values.yaml) | Configure data volume settings for the chart under this key. |
| persistence.export | object | See [values.yaml](./values.yaml) | Configure export volume settings for the chart under this key. |
| persistence.media | object | See [values.yaml](./values.yaml) | Configure media volume settings for the chart under this key. |
| redis | object | See [values.yaml](./values.yaml) | Enable and configure redis subchart under this key.    If enabled, the app's Redis env will be set for you.    [[ref]](https://github.com/bitnami/charts/tree/main/bitnami/redis) |
| service.main | object | See [values.yaml](./values.yaml) | Configures service settings for the chart. |
| tika.enabled | bool | `true` | Enable Tika sidecar |
| tika.image.pullPolicy | string | `"Always"` | Tika image pull policy |
| tika.image.repository | string | `"apache/tika"` | Tika image repository |
| tika.image.tag | string | `"3.1.0.0"` | Tika image tag |

---
Autogenerated from chart metadata using [helm-docs](https://github.com/norwoodj/helm-docs)
