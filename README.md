# github-readme-stats в Yandex cloud

Это адаптация проекта [github-readme-stats](https://github.com/anuraghazra/github-readme-stats) для облака Yandex, позволяющего выводить статистику в файлы `README.md`. В связи с ограничениями GitHub, при использовании github-readme-stats напрямую, не будет отображаться статистика по приватным репозиториям.

Данное решения укладывается в бесплатные лимиты Yandex Cloud и не требует вложения денежных средств.

## Перед началом работы

Зарегистрируйтесь в Yandex Cloud и создайте платежный аккаунт:

1. Перейдите в [консоль управления](https://console.cloud.yandex.com/), затем войдите в Yandex Cloud или зарегистрируйтесь, если вы еще не зарегистрированы.
2. [На странице биллинга](https://console.cloud.yandex.com/billing) убедитесь, что у вас подключен [платежный аккаунт](https://cloud.yandex.ru/docs/billing/concepts/billing-account), и он находится в статусе `ACTIVE` или `TRIAL_ACTIVE`. Если платежного аккаунта нет, [создайте его](https://cloud.yandex.ru/docs/billing/quickstart/).

Если у вас есть активный платежный аккаунт, вы можете создать или выбрать каталог, в котором будет работать ваша инфраструктура, на странице облака.

[Подробнее об облаках и каталогах](https://cloud.yandex.ru/docs/resource-manager/concepts/resources-hierarchy).

---

## Подготовьте ресурсы

1. Скачайте архив [github-stats-api.zip](backend/functions/github-stats-api/github-stats-api.7z).
2. [Создайте](https://cloud.yandex.ru/docs/iam/operations/sa/create) сервисный аккаунт и [назначьте ему роль](https://cloud.yandex.ru/docs/iam/operations/sa/assign-role-for-sa) `admin` на ваш каталог.

---

## [Создайте функцию](https://cloud.yandex.ru/docs/functions/operations/function/function-create)

-   Имя: github-stats-api

---

## [Создайте версию функции](https://cloud.yandex.ru/docs/functions/operations/function/version-manage)

-   Среда выполнения: Node.js 16.
-   Способ: ZIP archive.
-   Файл: github-stats-api.zip.
-   Точка входа: index.handler.
-   Таймаут: 7 sec.
-   Память: 128 MB.
-   [Сервисный аккаунт](https://cloud.yandex.ru/docs/iam/concepts/users/service-accounts): Your service account.
-   [Переменные окружения](https://cloud.yandex.ru/docs/functions/concepts/runtime/environment-variables): PAT_1 = '[токен для доступа в GitHub](https://github.com/settings/tokens/new), enable `repo` and `user` access'

---

## [Создайте API-шлюз](https://cloud.yandex.ru/docs/api-gateway/operations/api-gw-create)

-   Имя: github-stats-api

-   подготовьте спецификацию `specification.yaml`:

1. замените все <function_id> вашим идентификатором функции
2. замените все <service_account_id> вашим идентификатором сервисного аккаунта

-   Скопируйте спецификацию и вставьте в секцию со спецификацией в консоли Яндекса

---

# Deployment solution in Yandex cloud for github-readme-stats

This is an adaptation of the [github-readme-stats](https://github.com/anuraghazra/github-readme-stats) project for the Yandex cloud, which allows displaying statistics in `README.md` files. Due to GitHub limitations, using github-readme-stats directly will not show statistics for private repositories.

This solution is within the free limits of Yandex Cloud and does not require any investment.

## Getting started

Before you start, sign up for Yandex Cloud and create a billing account:

1. Go to the [management console](https://console.cloud.yandex.com/) and log in to Yandex Cloud or register if you don't have an account yet.
2. [On the billing page](https://console.cloud.yandex.com/billing), make sure you linked a [billing account](https://cloud.yandex.com/en/docs/billing/concepts/billing-account) and it has the `ACTIVE` or `TRIAL_ACTIVE` status. If you don't have a billing account, [create one](https://cloud.yandex.com/en/docs/billing/quickstart/).

If you have an active billing account, you can go to the cloud page to create or select a folder to run your infrastructure.

[Learn more about clouds and folders](https://cloud.yandex.com/en/docs/resource-manager/concepts/resources-hierarchy).

---

## Prepare resources

Download the [github-stats-api.zip](backend/functions/github-stats-api/github-stats-api.7z) archive.
[Create](https://cloud.yandex.com/en/docs/iam/operations/sa/create) a service account and [assign](https://cloud.yandex.com/en/docs/iam/operations/sa/assign-role-for-sa) it admin roles for your directory.

---

## [Create a function](https://cloud.yandex.com/en/docs/functions/operations/function/function-create)

-   Name: github-stats-api

---

## [Create Function Version](https://cloud.yandex.com/en/docs/functions/operations/function/version-manage)

-   Runtime environment: Node.js 16.
-   Method: ZIP archive.
-   File: github-stats-api.zip.
-   Entry point: index.handler.
-   Timeout: 7 sec.
-   RAM: 128 MB.
-   [Service account](https://cloud.yandex.com/en/docs/iam/concepts/users/service-accounts): Your service account.
-   [Environment variables](https://cloud.yandex.com/en/docs/functions/concepts/runtime/environment-variables): PAT_1 = '[token to access github](https://github.com/settings/tokens/new), enable `repo` and `user` access'

---

## [Creating API gateways](https://cloud.yandex.com/en/docs/api-gateway/operations/api-gw-create)

-   Name: github-stats-api

-   prepare specification `spec.yaml`:

1. replace all <function_id> with your function id
2. replace all <service_account_id> with your service account id

-   Copy specification and paste in the Specification section
