---
exo__Asset_uid: 7feb5d84-ab4a-495e-b0d8-edae41ab69db
exo__Asset_isDefinedBy: "[[e4920222-66a9-4103-9a4b-13d0a9e2d381]]"
exo__Asset_createdAt: 2026-06-14T04:46:34+05:00
exo__Asset_updatedAt: 2026-09-12T15:20:32
exo__Instance_class:
  - "[[73bd00e4-ccc0-4f3f-b20d-c4388c4588fb]]"
exo__Asset_label: "kitelev/exoas-shared-identities"
exo__AssetSpace_source: "https://github.com/kitelev/exoas-shared-identities"
exo__AssetSpace_namespace: "shared-identities"
exo__AssetSpace_dependsOn:
  - "[[f80bb130-7d05-4399-8407-467be8bfbfc9|exoas-public]]"
  - "[[511d9927-8409-43bb-809c-606e270baaa9|exoas-concept]]"
  - "[[8dec0e59-5914-46bd-9ea3-906f36cb5322|exoas-person]]"
  - "[[b2ac94ac-8ab2-4836-af58-7dc859630c99|exoas-agent]]"
  - "[[be4d6411-b951-42fe-826a-d55ab93a7acb|exoas-ztlk]]"
aliases:
  - "$shared-identities AssetSpace"
exo__AssetSpace_dependsOnKind: "[[e1d7fb5c-d334-448d-935b-953b7b033e78]]"
---
exo__AssetSpace descriptor for `kitelev/exoas-shared-identities` (EKA registry, D18 dependsOn). Holds foundational shared-identity TBox + concept classes referenced by leaf ABox.

> ⛔ **2026-09-12 (F4.4 / M3, узел `1a1b20e3`): УТВЕРЖДЕНИЕ ВЫШЕ ИСПРАВЛЕНО, прежняя редакция показана.**
> ⛔ Было: «concept classes (concept/**lit**/**ztlk** metaclasses, e.g. `lit__WebPage`)». Оба примера стали ложными: namespace `lit` поднят в `kitelev/exoas-lit` узлом `F3.4` (включая «сбежавший» `lit__WebPage`, физически лежавший здесь), namespace `ztlk` — в `kitelev/exoas-ztlk` узлом `F4.3` (`ztlk__Concept`, `ztlk__FleetingNoteType`, `ztlk__PermanentNote` уехали отсюда).
> ✅ Что осталось фактом: этот ассетспейс **ссылается** на оба namespace, но больше не **держит** их. Замер яруса определений `[три каноничных vault]`, `--no-cache`: `exoas-shared-identities → exoas-ztlk` = **2** трипла `exo__Class_superClass` (`Advice → ztlk__PermanentNote`, `Lifehack → ztlk__PermanentNote`) ⇒ `dependsOn → exoas-ztlk` объявлен этой же правкой; `exoas-shared-identities → exoas-lit` = **1** трипл `exo__Class_superClass` — ⛔ и он НЕ объявлен, потому что лежит ВНЕ области этого узла (рёбра бывшего цикла); он входит в остаток 52, заведённый отдельным тикетом.
 dependsOn `exoas-public` (its concept-instances use public concept TBox). Mount path `assetspaces/kitelev/exoas-shared-identities/`.
