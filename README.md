# VegaSystem / INNOVEGA - Documentation Backend et Flutter

Ce fichier explique le systeme VegaSystem / INNOVEGA en francais et en arabe.
Il couvre le backend NestJS, l'application mobile Flutter, les services principaux,
les routes API et le role de chaque fonction importante.

هذا الملف يشرح نظام VegaSystem / INNOVEGA بالفرنسية والعربية.
يشمل Backend المبني ب NestJS، تطبيق Flutter، الخدمات الرئيسية، واجهات API، ودور كل دالة مهمة.

---

## 1. Vue generale du systeme / نظرة عامة على النظام

### Francais

VegaSystem est une plateforme IoT pour l'agriculture intelligente. Elle permet de
surveiller et controler des passerelles, vannes, pompes et capteurs via MQTT,
MongoDB, API REST, WebSocket et une application mobile Flutter.

Les objectifs principaux sont :

- authentifier les utilisateurs et administrateurs ;
- gerer les passerelles, controleurs, capteurs et fabricants ;
- envoyer des commandes MQTT vers les noeuds IoT ;
- recevoir les paquets de retour des passerelles ;
- afficher les donnees en temps reel dans l'application mobile ;
- planifier l'irrigation ;
- utiliser l'IA pour recommandations, maladies des plantes, anomalies et consommation d'eau ;
- envoyer des notifications et alertes.

### العربية

VegaSystem هو نظام IoT للفلاحة الذكية. يمكن من مراقبة والتحكم في البوابات
والصمامات والمضخات والحساسات باستعمال MQTT و MongoDB و REST API و WebSocket
وتطبيق Flutter.

الأهداف الرئيسية هي:

- تسجيل دخول المستخدمين والمديرين ؛
- إدارة البوابات، المتحكمات، الحساسات والمصنعين ؛
- إرسال أوامر MQTT إلى أجهزة IoT ؛
- استقبال رسائل الرجوع من البوابات ؛
- عرض البيانات في الوقت الحقيقي داخل تطبيق الهاتف ؛
- برمجة الري ؛
- استعمال الذكاء الاصطناعي للتوصيات، أمراض النباتات، كشف الشذوذ واستهلاك الماء ؛
- إرسال التنبيهات والإشعارات.

---

## 2. Architecture / البنية العامة

```text
PFE/
  vegasystem/
    backend/              Backend NestJS + MongoDB + MQTT + WebSocket
    frontend/             Interface web React/Vite
    docker-compose.yaml   MongoDB, Mosquitto, backend, frontend
    mosquitto/            Configuration broker MQTT
    mongodb/              Scripts et donnees MongoDB

  innovega/
    innovega_app/         Application mobile Flutter
      lib/
        config/           Configuration, themes, traductions
        models/           Modeles de donnees
        screens/          Ecrans Flutter
        services/         Appels API, IA, sockets, stockage
        widgets/          Composants reutilisables
        utils/            Helpers et validation
```

### العربية

```text
PFE/
  vegasystem/
    backend/              الخادم الخلفي NestJS + MongoDB + MQTT + WebSocket
    frontend/             واجهة ويب React/Vite
    docker-compose.yaml   تشغيل MongoDB و Mosquitto و Backend و Frontend
    mosquitto/            إعدادات MQTT broker
    mongodb/              سكريبتات وبيانات MongoDB

  innovega/
    innovega_app/         تطبيق Flutter للهاتف
      lib/
        config/           الإعدادات، الثيم، الترجمات
        models/           نماذج البيانات
        screens/          الشاشات
        services/         API، IA، Socket، تخزين
        widgets/          عناصر واجهة قابلة لإعادة الاستعمال
        utils/            أدوات مساعدة والتحقق
```

---

## 3. Backend VegaSystem / الخادم الخلفي VegaSystem

### 3.1 Technologies / التقنيات

| Technologie | Francais | العربية |
| --- | --- | --- |
| NestJS | Framework backend Node.js organise en modules, controllers et services. | إطار عمل Backend مبني على Node.js ومنظم إلى Modules و Controllers و Services. |
| MongoDB + Mongoose | Stockage des utilisateurs, passerelles, controleurs, capteurs, historiques et notifications. | تخزين المستخدمين، البوابات، المتحكمات، الحساسات، السجلات والتنبيهات. |
| MQTT | Communication temps reel avec les gateways et noeuds IoT. | تواصل لحظي مع بوابات وأجهزة IoT. |
| Socket.io | Envoi des evenements temps reel vers l'application. | إرسال الأحداث في الوقت الحقيقي للتطبيق. |
| Swagger | Documentation automatique des APIs sur `/documentation`. | توثيق تلقائي للواجهات على `/documentation`. |
| JWT | Securisation des routes protegees. | حماية الواجهات باستعمال Token. |

### 3.2 Commandes de lancement / أوامر التشغيل

#### Backend seul / تشغيل Backend فقط

```bash
cd vegasystem/backend
npm install
npm run dev
```

#### Avec Docker / باستعمال Docker

```bash
cd vegasystem
docker compose up -d
```

Services par defaut :

- Backend API : `http://localhost:3000`
- Swagger : `http://localhost:3000/documentation`
- Frontend web : `http://localhost:4000`
- MongoDB : `localhost:27017`
- MQTT Mosquitto : `localhost:1884`

---

## 4. Backend - modules et fonctions / وحدات ودوال Backend

### 4.1 `main.ts`

| Fonction | Francais | العربية |
| --- | --- | --- |
| `bootstrap()` | Demarre l'application NestJS, active les fichiers statiques `/uploads`, configure CORS, cree Swagger et lance le serveur sur le port 3000. | تشغل تطبيق NestJS، تفعل ملفات `/uploads`، تضبط CORS، تنشئ Swagger وتشغل الخادم على المنفذ 3000. |

### 4.2 `app.module.ts`

| Fonction / element | Francais | العربية |
| --- | --- | --- |
| `imports` | Charge les modules principaux : MQTT, Auth, Users, Scheduling, Socket, Gateway, Controller, Sensor, Notification, Automation, DiseaseDetection et Feedback. | يحمل الوحدات الرئيسية: MQTT، المصادقة، المستخدمون، البرمجة، Socket، البوابات، المتحكمات، الحساسات، التنبيهات، الأتمتة، كشف الأمراض والتقييمات. |
| `MongooseModule.forRootAsync()` | Lit `MONGO_URL` depuis les fichiers `.env` et connecte MongoDB. | يقرأ `MONGO_URL` من ملفات `.env` ويتصل بقاعدة MongoDB. |
| `onModuleInit()` | Affiche la configuration MongoDB au demarrage pour verifier l'environnement. | يطبع إعدادات MongoDB عند التشغيل للتحقق من البيئة. |

---

## 5. Authentification / المصادقة

Fichiers :

- `vegasystem/backend/src/auth/auth.controller.ts`
- `vegasystem/backend/src/auth/auth.service.ts`

### Routes et fonctions

| Route / fonction | Francais | العربية |
| --- | --- | --- |
| `POST /auth/login` -> `login()` | Verifie email/mot de passe et retourne un JWT avec les donnees utilisateur. | يتحقق من البريد وكلمة المرور ويرجع JWT مع بيانات المستخدم. |
| `POST /auth/forgot-password` -> `forgotPassword()` | Cherche l'utilisateur par email, genere un token temporaire et envoie un email de reinitialisation. | يبحث عن المستخدم بالبريد، ينشئ رمزا مؤقتا ويرسل بريد إعادة تعيين كلمة المرور. |
| `POST /auth/reset-password` -> `resetPassword()` | Verifie le token, controle la longueur du mot de passe et met a jour le mot de passe. | يتحقق من الرمز، يفحص طول كلمة المرور ثم يحدثها. |
| `POST /auth/profile` -> `getProfile()` | Retourne le profil du token JWT courant. | يرجع ملف المستخدم الحالي من JWT. |
| `validateUser(email, pass)` | Compare le mot de passe recu avec le mot de passe stocke. | يقارن كلمة المرور المدخلة مع المخزنة. |
| `generateResetToken(userId)` | Cree un JWT limite dans le temps pour la reinitialisation. | ينشئ JWT محدود الوقت لإعادة تعيين كلمة المرور. |
| `verifyResetToken(token)` | Verifie que le token est valide et reserve a la reinitialisation. | يتحقق أن الرمز صالح ومخصص لإعادة كلمة المرور. |

---

## 6. Gestion des utilisateurs / إدارة المستخدمين

Fichiers :

- `src/user/user.controller.ts`
- `src/user/user.service.ts`

| Fonction | Francais | العربية |
| --- | --- | --- |
| `create()` | Cree un nouvel utilisateur, avec image optionnelle et mot de passe securise. | ينشئ مستخدما جديدا مع صورة اختيارية وكلمة مرور مؤمنة. |
| `findAll()` | Retourne la liste des utilisateurs. | يرجع قائمة المستخدمين. |
| `findOne()` / `findOneUser()` | Retourne un utilisateur par identifiant. | يرجع مستخدما حسب المعرف. |
| `findByEmail()` | Cherche un utilisateur par email. | يبحث عن مستخدم عبر البريد. |
| `validateUser()` | Verifie les informations de connexion. | يتحقق من معلومات الدخول. |
| `toggleBlocked()` | Bloque ou debloque un utilisateur. | يحظر أو يرفع الحظر عن مستخدم. |
| `deleteUser()` | Supprime un utilisateur. | يحذف مستخدما. |
| `update()` | Met a jour un utilisateur par l'administrateur. | يحدث بيانات مستخدم بواسطة المدير. |
| `findOwnProfile()` | Retourne le profil de l'utilisateur connecte. | يرجع ملف المستخدم المتصل. |
| `updateOwnProfile()` | Met a jour le profil personnel. | يحدث الملف الشخصي. |
| `updatePassword()` | Change le mot de passe directement. | يغير كلمة المرور مباشرة. |
| `updateOwnPassword()` | Verifie l'ancien mot de passe puis applique le nouveau. | يتحقق من كلمة المرور القديمة ثم يطبق الجديدة. |

---

## 7. MQTT et IoT / MQTT و IoT

Fichiers :

- `src/mqtt/mqtt.controller.ts`
- `src/mqtt/mqtt.service.ts`

### Routes principales

| Route / fonction | Francais | العربية |
| --- | --- | --- |
| `GET /mqtt/lora/user/:user/cloud/gwy` -> `getGwyList()` | Retourne les gateways accessibles par email utilisateur ou collaborateur. | يرجع البوابات المتاحة للمستخدم أو المتعاون عبر البريد. |
| `GET /mqtt/lora/gwy/:gatewayId/cloud/config` -> `getCloudNodesConfig()` | Retourne les noeuds d'une gateway groupes par section pour l'application. | يرجع أجهزة البوابة مجمعة حسب القسم للتطبيق. |
| `POST /mqtt/lora/gwy/:gatewayId/cloud/cmd` -> `processCommands()` | Recoit des commandes HTTP et les transforme en commandes MQTT. | يستقبل أوامر HTTP ويحولها إلى أوامر MQTT. |
| `POST /mqtt/lora/gwy/:gatewayId/cloud/schedule/:idNode` -> `addSchedule()` | Enregistre une planification pour un noeud. | يسجل برنامج ري لجهاز معين. |
| `POST /mqtt/lora/gwy/:gatewayId/cloud/group/schedule` -> `addManySchedules()` | Applique une meme planification a plusieurs noeuds. | يطبق نفس برنامج الري على عدة أجهزة. |
| `GET /mqtt/lora/gwy/:gatewayId/cloud/flow` -> `getFlowSensorsByGwy()` | Retourne les capteurs de debit d'une gateway. | يرجع حساسات تدفق الماء الخاصة ببوابة. |
| `POST /mqtt/lora/gwy/:gatewayId/cloud/reset-node` -> `resetNode()` | Envoie une commande de fermeture/reset vers un noeud. | يرسل أمر إغلاق أو إعادة تهيئة لجهاز. |

### Fonctions internes MQTT

| Fonction | Francais | العربية |
| --- | --- | --- |
| `setupClientEvents()` | Configure les evenements MQTT : connexion, erreur, offline, reconnexion. | يضبط أحداث MQTT: الاتصال، الخطأ، الانقطاع، إعادة الاتصال. |
| `initializeSubscriptions()` | Charge toutes les gateways et s'abonne aux topics MQTT de leurs paquets. | يحمل كل البوابات ويشترك في مواضيع MQTT الخاصة برسائلها. |
| `subscribeToNodesPacket(gatewayId)` | S'abonne au topic `lora/gwy/<gatewayId>/node/packet` et traite chaque message JSON. | يشترك في موضوع رسائل الأجهزة ويعالج كل رسالة JSON. |
| `getMqttNodesConfig(gatewayId)` | Prepare une configuration simplifiee pour la gateway : `idNode`, `status`, `type`. | يجهز إعدادات مختصرة للبوابة: معرف الجهاز، الحالة والنوع. |
| `publishNodesConfig(gatewayId)` | Publie la configuration des noeuds sur le topic MQTT `cloud/config`. | ينشر إعدادات الأجهزة على موضوع MQTT `cloud/config`. |
| `updateSensorValues(data)` | Met a jour les valeurs capteurs dans MongoDB et emet un evenement temps reel. | يحدث قيم الحساسات في MongoDB ويرسل حدثا لحظيا. |
| `emitIncomingPacket()` | Declenche un evenement interne pour WebSocket et autres services. | يطلق حدثا داخليا ل WebSocket وبقية الخدمات. |
| `setControllerStatus()` | Met a jour l'etat ouvert/ferme d'un noeud seulement si la valeur change. | يحدث حالة الجهاز مفتوح/مغلق فقط عند وجود تغيير. |
| `updateAliveController()` | Met a jour le champ `alive` d'un noeud. | يحدث حقل الاتصال `alive` لجهاز. |
| `handleStateGwyPacket()` | Traite un accusé de reception gateway vivante. | يعالج رسالة تؤكد أن البوابة تعمل. |
| `handleAckNodeStatusPacket()` | Traite l'accuse d'un noeud et synchronise son status. | يعالج تأكيد الجهاز ويزامن حالته. |
| `handleSensorPacket()` | Traite les donnees capteurs et envoie `ACK_SENSORS_NODE`. | يعالج بيانات الحساسات ويرسل تأكيدا. |
| `handleSubIdNode()` | Applique une action aux sous-noeuds derives d'un noeud principal. | يطبق إجراء على الأجهزة الفرعية التابعة لجهاز رئيسي. |
| `handleNodeOnlinePacket()` | Recupere un noeud apres redemarrage selon priorite et dependances. | يعيد مزامنة الجهاز بعد رجوعه للعمل حسب الأولوية والاعتماديات. |
| `handleNodeStatePacket()` | Compare l'etat recu avec la base et corrige les incoherences. | يقارن الحالة المستقبلة مع قاعدة البيانات ويصحح الاختلافات. |
| `handleErrorPacket()` | Interprete les codes d'erreur gateway/noeud et met a jour `alive` si necessaire. | يفسر رموز أخطاء البوابة/الجهاز ويحدث `alive` عند الحاجة. |
| `processPacket()` | Route chaque paquet MQTT vers le bon handler selon `packet`. | يوجه كل رسالة MQTT إلى المعالج المناسب حسب `packet`. |
| `sendCommands()` | Publie directement des commandes MQTT sans validation avancee. | ينشر أوامر MQTT مباشرة بدون تحقق متقدم. |
| `processCommands()` | Valide les commandes, utilise `NormalOpenCloseService` pour ouvrir/fermer, puis publie MQTT. | يتحقق من الأوامر، يستعمل خدمة الفتح/الغلق، ثم ينشر MQTT. |
| `addSchedule()` | Enregistre le planning dans le document controller. | يسجل برنامج الري داخل وثيقة المتحكم. |
| `resetNode()` | Envoie une commande de fermeture et attend la reponse du noeud. | يرسل أمر إغلاق وينتظر جواب الجهاز. |

---

## 8. Controleurs, passerelles et capteurs / المتحكمات والبوابات والحساسات

### `ControllerService`

| Fonction | Francais | العربية |
| --- | --- | --- |
| `create()` | Cree un controller/noeud. | ينشئ متحكما أو جهازا. |
| `findAll()` | Liste tous les controllers. | يعرض كل المتحكمات. |
| `findGroupedByGwys()` | Regroupe les controllers par gateway avec les infos gateway. | يجمع المتحكمات حسب البوابة مع معلوماتها. |
| `findOne(id, idGwy)` | Cherche un noeud par `idNode` et `gatewayId`. | يبحث عن جهاز بواسطة معرفه ومعرف البوابة. |
| `findByGwy(idGwy)` | Retourne tous les noeuds d'une gateway. | يرجع كل أجهزة بوابة معينة. |
| `update()` | Met a jour un noeud. | يحدث جهازا. |
| `remove()` | Supprime un noeud. | يحذف جهازا. |
| `disableSchedules()` | Desactive temporairement un planning du jour. | يعطل مؤقتا برنامج ري خاصا باليوم. |
| `makeKey()` | Cree une cle unique `gatewayId:controllerId`. | ينشئ مفتاحا فريدا من معرف البوابة والجهاز. |
| `pauseCronController()` | Ajoute un controller a la liste des crons pauses. | يضيف جهازا إلى قائمة البرامج الموقوفة. |
| `stopScheduleProcess()` | Met en pause les plannings d'une section. | يوقف برامج الري لقسم معين. |

### CRUD standards

Les modules suivants suivent un CRUD classique :

- `GatewayService` : `create`, `findAll`, `findOne`, `update`, `remove`
- `SensorService` : `create`, `findAll`, `findOne`, `findByName`, `update`, `remove`
- `ManufactoryService` : `create`, `findAll`, `findOne`, `update`, `remove`
- `ContinentService` : `createContinent`, `getAll`, `addCountry`, `addRegion`, `addCountryWithRegions`, `updateCountry`, `updateRegion`, `deleteCountry`, `deleteRegion`

### العربية

هذه الوحدات تستعمل عمليات CRUD الكلاسيكية:

- إنشاء عنصر جديد ؛
- جلب كل العناصر ؛
- جلب عنصر واحد ؛
- تحديث عنصر ؛
- حذف عنصر.

---

## 9. Notifications, action queue, maladies et feedback / التنبيهات والطابور والأمراض والتقييم

| Module | Fonctions importantes | Francais | العربية |
| --- | --- | --- | --- |
| `NotificationService` | `createNotification`, `getNotificationsByGatewayId`, `getUnreadNotificationsByGatewayId`, `markAsRead`, `sendNotification` | Gere les alertes, lues/non lues, canaux MQTT/email et emission WebSocket. | يدير التنبيهات، المقروءة وغير المقروءة، قنوات MQTT/email وإرسال WebSocket. |
| `ActionQueueService` | `enqueueScheduleNodeAction`, `getSnapshot`, `getHistory` | Suit les actions programmees et leur historique. | يتابع أوامر الري المبرمجة وتاريخها. |
| `DiseaseDetectionService` | `create`, `backfill`, `findMine`, `clearMine` | Sauvegarde et affiche l'historique des detections de maladies. | يحفظ ويعرض سجل كشف أمراض النباتات. |
| `FeedbackService` | `create`, `findAll`, `updateStatus` | Recoit les avis utilisateurs et permet a l'admin de changer leur statut. | يستقبل آراء المستخدمين ويسمح للمدير بتغيير حالتها. |
| `AutomationService` | `createConfig`, `findAllConfigs`, `findConfigById`, `findConfigByGwyAndSection`, `upsertByGatewayAndSection`, `updateState`, `removeConfig` | Gere les configurations IA par gateway et section. | يدير إعدادات الذكاء الاصطناعي حسب البوابة والقسم. |

---

## 10. Application Flutter INNOVEGA / تطبيق Flutter

### 10.1 Role de l'application / دور التطبيق

### Francais

L'application mobile est l'interface principale pour l'agriculteur et
l'administrateur. Elle affiche les donnees des gateways, permet l'ouverture et
fermeture des vannes/pompes, montre les capteurs, programme l'irrigation,
consulte les cartes, notifications, statistiques, IA et profil.

### العربية

تطبيق الهاتف هو الواجهة الرئيسية للفلاح والمدير. يعرض بيانات البوابات، يسمح
بفتح وغلق الصمامات والمضخات، يعرض الحساسات، يبرمج الري، يعرض الخرائط،
التنبيهات، الإحصائيات، الذكاء الاصطناعي والملف الشخصي.

### 10.2 Commandes Flutter / أوامر Flutter

```bash
cd innovega/innovega_app
flutter pub get
flutter run
flutter analyze
```

Pour choisir un backend :

```bash
flutter run --dart-define=API_BASE_URL=http://localhost:3000
flutter run --dart-define=ADMIN_BASE_URL=http://localhost:3000
flutter run --dart-define=AI_BASE_URL=https://elrabii.servehttp.com/ai
```

---

## 11. Flutter - fichiers principaux / الملفات الرئيسية

| Fichier | Francais | العربية |
| --- | --- | --- |
| `lib/main.dart` | Initialise Flutter, notifications, preferences, themes, routes et lance `MyApp`. | يهيئ Flutter، التنبيهات، التفضيلات، الثيم، المسارات ويشغل `MyApp`. |
| `lib/config/environment.dart` | Centralise les URLs backend, IA, ML, Disease AI et constantes globales. | يجمع روابط Backend و IA و ML و Disease AI والثوابت العامة. |
| `lib/config/design_system.dart` | Definit couleurs, typographie, espacements et ThemeData. | يحدد الألوان، الخطوط، المسافات والثيم. |
| `lib/config/app_translations.dart` | Contient les textes traduits utilises par l'application. | يحتوي على النصوص المترجمة في التطبيق. |
| `lib/screens/root_shell.dart` | Conteneur principal apres connexion : navigation, drawer et sockets. | الحاوية الرئيسية بعد الدخول: تنقل، قائمة جانبية و Socket. |
| `lib/screens/startup_screen.dart` | Decide si l'utilisateur va vers onboarding, PIN, login ou app. | يقرر هل المستخدم يذهب إلى الترحيب، PIN، الدخول أو التطبيق. |
| `lib/screens/dashboard_screen.dart` | Affiche les noeuds, capteurs, et commandes temps reel. | يعرض الأجهزة والحساسات وأوامر الوقت الحقيقي. |
| `lib/screens/admin_screen.dart` | Interface admin pour gerer users, gateways, sensors, controllers et zones. | واجهة المدير لإدارة المستخدمين والبوابات والحساسات والمتحكمات والمناطق. |
| `lib/screens/ai_mode_screen.dart` | Point d'entree des recommandations IA. | مدخل توصيات الذكاء الاصطناعي. |
| `lib/screens/disease_detection_screen.dart` | Detection maladie par image. | كشف مرض النبات بالصورة. |
| `lib/screens/agrobot_screen.dart` | Chatbot agricole AgroBot. | المساعد الزراعي AgroBot. |
| `lib/screens/map_screen.dart` | Carte OpenStreetMap des equipements. | خريطة OpenStreetMap للمعدات. |
| `lib/screens/google_maps_screen.dart` | Carte Google Maps alternative. | خريطة Google Maps بديلة. |
| `lib/screens/weather_screen.dart` | Meteo actuelle et previsions. | الطقس الحالي والتوقعات. |
| `lib/screens/water_consumption_screen.dart` | Analyse consommation eau et export PDF. | تحليل استهلاك الماء وتصدير PDF. |
| `lib/screens/settings_page.dart` | Profil, preferences, langue, theme, notifications et securite. | الملف الشخصي، التفضيلات، اللغة، الثيم، التنبيهات والأمان. |

---

## 12. Flutter services - explication des fonctions / شرح دوال خدمات Flutter

### 12.1 `AuthService`

| Fonction | Francais | العربية |
| --- | --- | --- |
| `login()` | Envoie email/password a `/auth/login` et retourne le token + user. | يرسل البريد وكلمة المرور إلى `/auth/login` ويرجع Token والمستخدم. |
| `getUserGateways()` | Charge les gateways de l'utilisateur connecte. | يجلب بوابات المستخدم المتصل. |
| `logout()` | Appelle la route de sortie si disponible. | يستدعي واجهة الخروج إن وجدت. |
| `updatePassword()` | Change le mot de passe depuis l'espace personnel. | يغير كلمة المرور من الحساب الشخصي. |
| `getProfile()` | Charge le profil connecte depuis `/users/me`. | يجلب الملف الشخصي من `/users/me`. |
| `updateProfile()` | Met a jour les champs profil via `MultipartRequest`. | يحدث بيانات الملف الشخصي عبر طلب متعدد الأجزاء. |
| `resetPassword()` | Envoie token + nouveau mot de passe. | يرسل الرمز وكلمة المرور الجديدة. |
| `requestPasswordReset()` | Demande l'envoi d'un lien de reinitialisation. | يطلب إرسال رابط إعادة تعيين كلمة المرور. |
| `refreshToken()` | Tente de renouveler le token. | يحاول تجديد Token. |
| `_extractErrorMessage()` | Lit un message d'erreur JSON ou retourne un fallback. | يقرأ رسالة خطأ JSON أو يرجع رسالة بديلة. |
| `_extractObject()` | Extrait l'objet utile depuis une reponse API. | يستخرج الكائن المفيد من جواب API. |

### 12.2 `DashboardService`

| Fonction | Francais | العربية |
| --- | --- | --- |
| `getGatewayConfig()` | Charge les sections et noeuds d'une gateway. | يجلب الأقسام والأجهزة الخاصة ببوابة. |
| `sendNodeCommand()` | Envoie OPEN/CLOSE vers une vanne ou pompe via `/cloud/cmd`. | يرسل أمر فتح/غلق لصمام أو مضخة عبر `/cloud/cmd`. |
| `rebootGateway()` | Envoie la commande MQTT de redemarrage gateway. | يرسل أمر إعادة تشغيل البوابة. |
| `resetNode()` | Demande au backend de remettre un noeud dans un etat ferme/securise. | يطلب من Backend إعادة الجهاز إلى حالة مغلقة/آمنة. |

### 12.3 `GatewayService`

| Fonction | Francais | العربية |
| --- | --- | --- |
| `getUserGateways()` | Recupere les gateways disponibles pour l'utilisateur. | يجلب البوابات المتاحة للمستخدم. |
| `getGatewayDetails()` | Recupere les details d'une gateway. | يجلب تفاصيل بوابة. |
| `getGatewayConfig()` | Recupere la configuration IoT d'une gateway. | يجلب إعدادات IoT لبوابة. |
| `_headers()` | Prepare les headers HTTP avec token si disponible. | يحضر Headers مع Token عند توفره. |
| `_preview()` | Limite l'affichage console des longues reponses. | يختصر عرض الأجوبة الطويلة في Console. |

### 12.4 `ScheduleService`

| Fonction | Francais | العربية |
| --- | --- | --- |
| `getSectionSchedule()` | Charge le planning d'une section. | يجلب برنامج الري لقسم. |
| `updateSchedule()` | Enregistre ou modifie le planning d'un noeud/section. | يحفظ أو يغير برنامج الري لجهاز/قسم. |
| `clearSchedules()` | Supprime les plannings d'un noeud. | يحذف برامج الري لجهاز. |
| `disableSchedules()` | Desactive temporairement un planning actif. | يعطل مؤقتا برنامجا نشطا. |

### 12.5 `AiService`

| Fonction | Francais | العربية |
| --- | --- | --- |
| `getPlants()` | Charge la liste des plantes disponibles pour l'IA. | يجلب قائمة النباتات المتاحة للذكاء الاصطناعي. |
| `getCountries()` | Charge les pays disponibles pour les modeles/meteo. | يجلب البلدان المتاحة للنماذج/الطقس. |
| `getStations()` | Charge les stations meteo. | يجلب محطات الطقس. |
| `getSectionConfig()` | Lit la configuration IA d'une gateway/section. | يقرأ إعداد IA لبوابة/قسم. |
| `getAllSectionConfigs()` | Recupere toutes les configurations IA. | يجلب كل إعدادات IA. |
| `createSectionConfig()` | Cree une configuration IA. | ينشئ إعداد IA. |
| `updateSectionConfig()` | Modifie une configuration IA par identifiant. | يحدث إعداد IA بواسطة المعرف. |
| `upsertSectionConfigByGatewayAndSection()` | Cree ou met a jour selon gateway + section. | ينشئ أو يحدث حسب البوابة والقسم. |
| `deleteSectionConfig()` | Supprime une configuration IA. | يحذف إعداد IA. |
| `calculateIrrigation()` | Appelle le moteur IA de calcul d'irrigation et valide les resultats. | يستدعي محرك IA لحساب الري ويتحقق من النتائج. |
| `updateSectionStatus()` | Change le statut d'une configuration IA. | يغير حالة إعداد IA. |
| `detectDiseaseImage()` | Envoie une image au service IA maladie. | يرسل صورة إلى خدمة كشف المرض. |
| `getDiseaseTreatmentRecommendations()` | Recupere les traitements recommandes pour une maladie. | يجلب العلاجات المقترحة لمرض. |
| `getDiseaseDetectionHistory()` | Charge l'historique des detections sauvegardees. | يجلب سجل كشوفات المرض. |
| `saveDiseaseDetection()` | Sauvegarde une detection dans le backend. | يحفظ كشفا في Backend. |
| `backfillDiseaseDetectionHistory()` | Synchronise plusieurs detections locales vers le backend. | يزامن عدة كشوفات محلية مع Backend. |
| `clearDiseaseDetectionHistory()` | Supprime l'historique des detections. | يحذف سجل الكشوفات. |

### 12.6 Services temps reel et notifications

| Service / fonction | Francais | العربية |
| --- | --- | --- |
| `SocketService.init()` | Initialise socket.io avec URL backend et token. | يهيئ Socket.io برابط Backend و Token. |
| `SocketService.watchRoom()` | Ecoute une room gateway. | يستمع لغرفة بوابة معينة. |
| `SocketService.joinGateway()` / `leaveGateway()` | Entre ou sort d'un canal gateway. | يدخل أو يخرج من قناة بوابة. |
| `SocketService.onNotification()` | Enregistre un callback pour notifications. | يسجل دالة استقبال التنبيهات. |
| `SocketService.dispose()` | Ferme socket et nettoie les callbacks. | يغلق Socket وينظف callbacks. |
| `PollingNotificationService.startPolling()` | Lance une verification periodique des notifications. | يبدأ فحصا دوريا للتنبيهات. |
| `PollingNotificationService.markAsRead()` | Marque une notification comme lue. | يجعل التنبيه مقروءا. |
| `NotificationService` | Gere stockage local, compteur non lu et affichage des alertes. | يدير التخزين المحلي، عداد غير المقروء وعرض التنبيهات. |

### 12.7 Services stockage et preferences

| Service / fonction | Francais | العربية |
| --- | --- | --- |
| `StorageService.init()` | Initialise `SharedPreferences`. | يهيئ التخزين المحلي `SharedPreferences`. |
| `saveLoginData()` | Sauvegarde user, token et refresh token. | يحفظ المستخدم و Token و Refresh Token. |
| `getSavedUser()` | Retourne l'utilisateur sauvegarde. | يرجع المستخدم المخزن. |
| `saveSelectedGateway()` | Sauvegarde la gateway choisie. | يحفظ البوابة المختارة. |
| `isLoggedIn()` | Verifie si une session locale existe. | يتحقق من وجود جلسة محلية. |
| `clearAllData()` | Supprime les donnees locales de session. | يحذف بيانات الجلسة المحلية. |
| `PreferencesService.init()` | Charge les preferences utilisateur. | يحمل تفضيلات المستخدم. |
| `savePreferences()` | Sauvegarde toutes les preferences. | يحفظ كل التفضيلات. |
| `updateLanguage()` | Change la langue. | يغير اللغة. |
| `updateTheme()` | Change le theme. | يغير الثيم. |
| `updateNotifications()` | Active/desactive les notifications. | يفعل أو يعطل التنبيهات. |
| `resetToDefaults()` | Remet les preferences par defaut. | يعيد التفضيلات الافتراضية. |

### 12.8 Services IA, voix, cartes et rapports

| Service / fonction | Francais | العربية |
| --- | --- | --- |
| `AgroBotApiService.sendMessage()` | Envoie une question au service AgroBot. | يرسل سؤالا إلى خدمة AgroBot. |
| `SmartChatbotService.replyHybrid()` | Combine IA/API et contexte ferme pour repondre. | يجمع IA/API وسياق المزرعة للإجابة. |
| `SmartChatbotService.replyNlpOnly()` | Repond uniquement avec le modele NLP local. | يجيب فقط باستعمال نموذج NLP المحلي. |
| `CommandParserService` | Transforme une phrase en commande de controle. | يحول الجملة إلى أمر تحكم. |
| `SpeechToTextService.startListening()` | Demarre la reconnaissance vocale. | يبدأ التعرف على الصوت. |
| `TextToSpeechService.speak()` | Lit un texte vocalement. | ينطق النص صوتيا. |
| `VoiceCommandService.parseTranscript()` | Analyse le texte vocal transcrit. | يحلل النص الناتج من الصوت. |
| `MapService` | Prepare et gere les positions des appareils. | يجهز ويدير مواقع الأجهزة. |
| `LocationService` | Recupere la position GPS. | يجلب موقع GPS. |
| `WeatherService.getCurrentWeather()` | Charge la meteo actuelle. | يجلب الطقس الحالي. |
| `WeatherService.getForecast()` | Charge les previsions. | يجلب التوقعات. |
| `WaterConsumptionService.getWaterConsumption()` | Charge les donnees de consommation eau. | يجلب بيانات استهلاك الماء. |
| `PdfGenerationService.buildWeatherReportPdf()` | Genere un rapport PDF meteo. | ينشئ تقرير PDF للطقس. |
| `PdfGenerationService.buildWaterConsumptionReportPdf()` | Genere un rapport PDF de consommation eau. | ينشئ تقرير PDF لاستهلاك الماء. |
| `SecurityPinService.verifyPin()` | Verifie le PIN local. | يتحقق من رمز PIN المحلي. |
| `FeedbackService` | Envoie les retours utilisateurs au backend. | يرسل ملاحظات المستخدم إلى Backend. |

---

## 13. Flutter screens - role des fonctions privees / دور دوال الشاشات

Dans les ecrans Flutter, beaucoup de fonctions commencent par `_build...`,
`_load...`, `_refresh...`, `_open...`, `_save...` ou `_format...`.

### Francais

- `_build...` : construit une partie de l'interface graphique.
- `_load...` : charge les donnees depuis API ou stockage local.
- `_refresh...` : recharge les donnees apres une action utilisateur.
- `_open...` : ouvre une page, un dialogue ou un bottom sheet.
- `_save...` : sauvegarde une configuration ou un formulaire.
- `_format...` : transforme une valeur brute en texte lisible.
- `_validate...` : verifie les donnees avant envoi.
- `_execute...` : lance une action metier comme ouvrir une vanne ou appliquer un planning.

### العربية

- `_build...` : يبني جزءا من واجهة المستخدم.
- `_load...` : يجلب البيانات من API أو التخزين المحلي.
- `_refresh...` : يعيد تحميل البيانات بعد عملية من المستخدم.
- `_open...` : يفتح شاشة أو نافذة أو Bottom Sheet.
- `_save...` : يحفظ إعدادا أو نموذجا.
- `_format...` : يحول قيمة خام إلى نص مفهوم.
- `_validate...` : يتحقق من البيانات قبل الإرسال.
- `_execute...` : ينفذ عملية مثل فتح صمام أو تطبيق برنامج ري.

---

## 14. Flux principal / المسار الرئيسي للتطبيق

### Francais

1. `main.dart` initialise l'application.
2. `StartupScreen` verifie la session et le PIN.
3. `LoginScreen` appelle `AuthService.login()`.
4. `GatewaySelectionScreen` charge les gateways de l'utilisateur.
5. `RootShell` affiche la navigation principale.
6. `DashboardScreen` appelle `DashboardService.getGatewayConfig()`.
7. `SocketService` recoit les mises a jour temps reel.
8. L'utilisateur ouvre/ferme une vanne avec `sendNodeCommand()`.
9. Le backend publie la commande MQTT.
10. La gateway repond avec un paquet MQTT.
11. Le backend met a jour MongoDB et envoie un evenement WebSocket.
12. L'application met a jour l'interface.

### العربية

1. `main.dart` يهيئ التطبيق.
2. `StartupScreen` يتحقق من الجلسة و PIN.
3. `LoginScreen` يستدعي `AuthService.login()`.
4. `GatewaySelectionScreen` يجلب بوابات المستخدم.
5. `RootShell` يعرض التنقل الرئيسي.
6. `DashboardScreen` يستدعي `DashboardService.getGatewayConfig()`.
7. `SocketService` يستقبل تحديثات الوقت الحقيقي.
8. المستخدم يفتح أو يغلق صماما عبر `sendNodeCommand()`.
9. Backend ينشر الأمر عبر MQTT.
10. البوابة ترجع رسالة MQTT.
11. Backend يحدث MongoDB ويرسل WebSocket.
12. التطبيق يحدث الواجهة.

---

## 15. Protocole MQTT resume / ملخص بروتوكول MQTT

| Commande | Valeur | Francais | العربية |
| --- | --- | --- | --- |
| `CHECK_GWY` | `0` | Verifier si la gateway est vivante. | التحقق أن البوابة تعمل. |
| `CHANGE_STATUS_NODE` | `1` | Ouvrir ou fermer un noeud. | فتح أو غلق جهاز. |
| `GET_STATE_NODE` | `2` | Demander l'etat d'un noeud. | طلب حالة جهاز. |
| `GET_SENSORS_NODE` | `3` | Demander les valeurs capteurs. | طلب قيم الحساسات. |
| `SLEEP_NODE` | `5` | Mettre le noeud en veille. | وضع الجهاز في النوم. |
| `ACK_SENSORS_NODE` | `6` | Confirmer la reception des capteurs. | تأكيد استقبال بيانات الحساسات. |
| `REBOOT_GWY` | `7` | Redemarrer la gateway. | إعادة تشغيل البوابة. |
| `SETUP_GENERAL_NODE` | `8` | Configurer un noeud. | إعداد جهاز. |
| `SETUP_SENSORS_NODE` | `9` | Configurer un capteur sur un noeud. | إعداد حساس داخل جهاز. |
| `SETUP_GWY` | `10` | Configurer la gateway. | إعداد البوابة. |
| `CMD_RST_SETUP_GWY` | `11` | Reinitialiser la configuration gateway. | إعادة إعدادات البوابة. |
| `CMD_RST_SETUP_GENERAL_NODE` | `12` | Reinitialiser la configuration du noeud. | إعادة إعدادات الجهاز. |

---

## 16. Resume pour soutenance / ملخص للمناقشة

### Francais

INNOVEGA est une solution complete d'agriculture intelligente. Le backend NestJS
centralise les donnees, securise les utilisateurs, communique avec les gateways
par MQTT et diffuse les changements par WebSocket. L'application Flutter
consomme ces APIs, affiche les donnees en temps reel et donne a l'utilisateur
des outils de controle, planification, IA, meteo, cartographie et rapports.

### العربية

INNOVEGA هو حل متكامل للفلاحة الذكية. Backend المبني ب NestJS يجمع البيانات،
يحمي المستخدمين، يتواصل مع البوابات عبر MQTT ويرسل التحديثات عبر WebSocket.
تطبيق Flutter يستهلك هذه الواجهات، يعرض البيانات لحظيا، ويوفر للمستخدم التحكم،
البرمجة، الذكاء الاصطناعي، الطقس، الخرائط والتقارير.

