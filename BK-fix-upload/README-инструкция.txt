BKTitleGuard — патч для Banner Kings Redux v1.9.35.1
====================================================

Что это: пересборка BannerKings.dll с защитой от двух крашей:
1) краш старта новой игры (FeudalContract.PostInitialize — у героя-держателя титула null-культура);
   патч не только лечит, но и пишет в лог имя героя-виновника;
2) краш найма добровольцев на островных поселениях War Sails (BKVolunteerModel).

СОДЕРЖИМОЕ ПАПКИ
- FeudalContract.cs, FeudalTitle.cs, BKVolunteerModel.cs  -> в форк в папку bkfix/
- bkfix-build.yml                                          -> в форк в .github/workflows/
- README (этот файл)

ЧТО СДЕЛАТЬ (один раз, ~10 минут)
1. Скачай эту папку с Google Диска целиком (правый клик по папке -> Скачать), распакуй zip.
2. Открой свой форк: https://github.com/IrishPagan1/bannerlord-banner-kings-redux
3. Кнопка "Add file" -> "Upload files". Перетащи в область загрузки ДВЕ папки из архива:
   bkfix (три .cs) и .github (внутри workflows/bkfix-build.yml).
   Важно: тащить сами папки bkfix и .github, а не их общую родительскую.
   Если перетаскивание не сработает, вариант Б: "Add file" -> "Create new file",
   в поле имени вводишь путь со слэшами: bkfix/FeudalContract.cs (слэш создаёт папку),
   вставляешь содержимое файла, внизу "Commit changes". Повторить для:
   bkfix/FeudalTitle.cs, bkfix/BKVolunteerModel.cs, .github/workflows/bkfix-build.yml.
4. Вкладка "Actions". Если сверху плашка "Workflows aren't being run..." — нажать
   "I understand my workflows, go ahead and enable them". Сборка запустится сама
   (триггер — файлы bkfix/**). Если сама не побежала: слева "BK Guard Build" ->
   "Run workflow" -> "Run workflow".
5. Подождать 5-10 минут до зелёной галочки. Готовые файлы: справа "Releases" ->
   "v1.9.35.1-guard1" -> скачать BannerKings.dll и BannerKings.pdb.
   Запасной путь: сам прогон сборки -> внизу "Artifacts" -> BannerKings-guard.

УСТАНОВКА
1. В папке мода BannerKings (bin\Win64_Shipping_Client\) заменить ТОЛЬКО два файла:
   BannerKings.dll и BannerKings.pdb. RU-папку и правки XML НЕ трогать.
2. Правый клик по BannerKings.dll -> Свойства -> если есть галка "Разблокировать"
   (Unblock) — поставить, ОК.
3. Запустить игру, начать НОВУЮ песочницу.
4. Открыть C:\ProgramData\Mount and Blade II Bannerlord\logs\rgl_log.txt,
   найти строку [BKTitleGuard] — там имя героя-виновника
   (fief/title/deJure/name/culture/clan/kingdom). Пришли эту строку целиком.
5. Если игра дошла до карты — краш закрыт, можно играть. Строку всё равно пришли:
   оформим issue автору мода с точным виновником и фиксом.

Если сборка упала (красный крест): открой прогон, нажми на шаг с ошибкой,
скопируй последние ~40 строк лога и пришли мне — поправлю патч.