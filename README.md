# LLM Pre-Processing Guardrails: 
Layer 1 Defense This repository contains a practical demonstration of 
**Layer 1 (Pre-processing)** security defenses for Large Language Models. We test three distinct filtering mechanisms against Prompt Injection and data leakage attacks using the Yandex Cloud API (DeepSeek model).

## 🛡️ Goal To demonstrate that relying on the model's internal "Alignment" is insufficient. We implement an **Echeloned Defense (Defense in Depth)** to filter malicious inputs *before* they reach the LLM.
## 📋 Project Flow (What happened) 
1. **Baseline:** We confirmed that DeepSeek V4 has strong internal safety (Alignment) but can still be manipulated into providing "helpful" advice on malicious topics.
2. **Layer 1.1 — Delimiters:** We wrapped user input in `<USER_DATA>` tags. This created a "Semantic Sandbox," forcing the model to strictly reject code execution instructions found inside the data.
3. **Layer 1.2 — ML Classifier:** We deployed a lightweight `Naive Bayes` model as a "Gatekeeper." It failed to detect the injection (False Negative), proving that simple keyword-based ML is brittle.
4. **Layer 1.3 — PII Detector:** We used Regular Expressions to scan for sensitive data (Emails, Phones, Cards). This layer successfully blocked the request to prevent Data Loss (DLP).

 ## 📊 Key Findings (Conclusions) * **Delimiters > Alignment:** Explicitly marking data boundaries is more effective than relying on the model's "common sense." * **The "Alignment Tax":** There is a fundamental trade-off. Making a model "safer" often makes it less "capable" (flexible). * **Pre-processing is a Cascade:** No single filter is perfect. The ML Classifier failed, but the Delimiters and PII Detector saved the system. 
 
 ## 💻 Tech Stack * 
 **API:** Yandex Cloud (OpenAI-compatible) * 
 **Model:** DeepSeek V4 Flash * 
 **Env:** Google Colab * 
 **Libs:** `openai`, `scikit-learn`, `re`
 
 ## 📜 License 
 MIT


# LLM Pre-Processing Guardrails: Защита Уровня 1

Этот репозиторий содержит практическую демонстрацию **Уровня 1 (Pre-processing)** систем безопасности для больших языковых моделей. Мы тестируем три различных фильтра против атак Prompt Injection и утечек данных через API Yandex Cloud (модель DeepSeek).

## 🛡️ Цель
Показать, что полагаться только на внутреннюю "Согласованность" (Alignment) модели недостаточно. Мы внедряем **многоуровневую оборону (Defense in Depth)**, чтобы фильтровать вредоносные запросы *до* того, как они попадут в LLM.

## 📋 Ход событий
1.  **Базовый тест (Baseline):** Мы подтвердили, что DeepSeek V4 имеет сильное внутреннее выравнивание, но его можно обмануть, заставив давать "полезные" советы по вредоносным темам.
2.  **Уровень 1.1 — Delimiters:** Мы обернули ввод пользователя в теги `<USER_DATA>`. Это создало "Семантическую песочницу", заставив модель строго отклонять инструкции по выполнению кода, найденные внутри данных.
3.  **Уровень 1.2 — ML Classifier:** Мы развернули легкую модель `Naive Bayes` в роли "Привратника". Она пропустила инъекцию (False Negative), доказав, что простые классификаторы по ключевым словам хрупки.
4.  **Уровень 1.3 — PII Detector:** Мы использовали регулярные выражения для поиска чувствительных данных (Email, Телефоны, Карты). Этот слой успешно заблокировал запрос, предотвратив утечку данных (DLP).

## 📊 Выводы
*   **Метки важнее Согласованности:** Явное разделение "Кода" и "Данных" эффективнее, чем надежда на "здравый смысл" модели.
*   **"Налог на выравнивание" (Alignment Tax):** Существует фундаментальный конфликт. Чем "безопаснее" модель, тем она менее "способна" (гибка).
*   **Pre-processing — это каскад:** Ни один фильтр не идеален. ML-классификатор провалился, но Delimiters и PII Detector спасли систему.

## 💻 Стек технологий
*   **API:** Yandex Cloud (OpenAI-совместимый)
*   **Модель:** DeepSeek V4 Flash
*   **Среда:** Google Colab
*   **Библ:** `openai`, `scikit-learn`, `re`

## 📜 Лицензия
MIT
