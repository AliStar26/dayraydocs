---
sidebar_position: 3
---

# Документация по backend

Интеграция написана на языке ```C#``` с использованием технологии - [ASP NET CORE](https://learn.microsoft.com/ru-ru/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-5.0).
В проекте используются:

||
| :--- | :--- |
|EntityFramework| объектно-реляционный маппер (ORM) для .NET|
|Swagger| набор инструментов для создания, описания, документирования и тестирования REST API |
|JwtBearer| метод аутентификации, который использует токены JWT для идентификации пользователей |



1. Lapka-backend    - основной ASP NET CORE project, выполняющий интеграцию, содержит контроллеры API.
2. DTO(Data Transfer Object) - определяет данные для передачи, а также содержит репозитории.
3. Service - содержит в себе интерфейсы и их реализацию. 
