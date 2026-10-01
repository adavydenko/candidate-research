# Индекс идей — проект «Кандидатская»

> Назначение: сохранять все потенциально полезные исследовательские идеи, возникающие в ходе обсуждения кандидатской и смежных технических дискуссий.  
> Это **реестр идей, а не список обязательств**: идея может быть перспективной, вспомогательной, отложенной или отбракованной.
>
> Последнее обновление: 2026-09-13

## Как читать оценки

- **Перспективность**: 1–5, насколько идея кажется потенциально ценной как исследовательское направление.
- **Соответствие 1.2.2**: 1–5, насколько естественно идея ложится в «Математическое моделирование, численные методы и комплексы программ».
- **Зрелость**:
  - `набросок` — красивая мысль, почти не проверена;
  - `гипотеза` — есть постановка и аналоги;
  - `эксперимент` — можно ставить конкретный тест;
  - `кандидат в ядро` — потенциально может стать центральным результатом диссертации;
  - `вспомогательная` — полезна как baseline, инфраструктура или отдельная статья.

## Реестр

| ID | Тезис / рабочее название | Краткая постановка | Контекст / зачем | Возможная научная новизна | Аналоги / литература | Кто предложил | 1.2.2 | Персп. | Главный риск | Следующий дешевый эксперимент | Статус |
|---|---|---|---|---|---|---|---:|---:|---|---|---|
| I-001 | **FLLC как exact baseline / fallback** | Dependency-free lossless codec для float time series на основе delta coding и bit packing используется не как главная новизна, а как точный нижний уровень сравнения | Связать старую разработку с новой работой, не переоценивая ее новизну | Новизна скорее в роли внутри адаптивной многоуровневой схемы, а не в самом codec | Современные lossless float codecs; predictive/residual coding | AD | 4 | 3 | Сам FLLC, вероятно, не нов | Зафиксировать reproducible benchmark FLLC vs современные codecs | вспомогательная |
| I-002 | **Многоуровневое представление состояния** | `raw state → exact/compressed → latent → semantic → agent decision` | Общая архитектура, объединяющая старые и новые темы | Адаптивный выбор уровня представления по задаче и бюджету | Reduced-order modeling; semantic/task-oriented communication | совместно | 5 | 5 | Может стать слишком широкой рамкой без конкретного метода | Реализовать 3 уровня на одном временном ряду и построить Pareto-front | кандидат в ядро |
| I-003 | **Invariant-/task-preserving representation** | Сжимать/редуцировать состояние не по минимальному MSE, а по сохранению инвариантов, динамики и downstream-задачи | В физике точное сохранение всех float-битов не всегда равно сохранению физически важной информации | Определение эквивалентности состояний через `E_state`, `E_inv`, `E_dyn`, `E_task` | Structure-preserving ROM; QoI-aware scientific compression | совместно, исходный толчок AD | 5 | 5 | Одних инвариантов недостаточно для эквивалентности траекторий | N-body: сравнить MSE-optimized и invariant-aware representation по long-horizon drift | кандидат в ядро |
| I-004 | **Receiver-aware cumulative delta** | Передавать дельту не относительно предыдущей истинной точки, а относительно последнего подтвержденного состояния получателя | Позволяет пропускать несущественные отсчеты без разрыва delta-chain | Протокол накопленной коррекции с anchor/checkpoint и контролем рассинхронизации | Send-on-delta; event-triggered estimation | AD выявил проблему, решение совместно | 5 | 5 | Близко к известным event-triggered схемам — нужна четкая новизна | Симуляция: обычная delta-chain vs anchor-delta при редких отправках и packet loss | эксперимент |
| I-005 | **Predictive latent innovation** | Обе стороны прогнозируют следующее latent-state; передается только ошибка прогноза `e_t = z_t - ẑ_t(receiver)` | Еще сильнее уменьшает коммуникацию, если динамика предсказуема | Temporal latent innovation + adaptive correction + resync | Innovation/Kalman ideas; predictive coding; latent dynamics | совместно | 5 | 5 | Уже есть predictive/event-triggered estimation; комбинацию надо отличить | На N-body/рядe: shared predictor + latent innovation vs raw/anchor delta | кандидат в ядро |
| I-006 | **Learned significance gate** | Gate выбирает `ignore / latent update / exact correction / checkpoint` по состоянию, ошибке, задаче и бюджету | Отвечает на ключевой вопрос «когда изменение значимо?» | Обучаемая функция значимости с жесткими ограничениями на инварианты/ошибку/age | Dynamic event-triggered control; task-oriented comms | совместно | 5 | 5 | Без ограничений может быть «еще один classifier» | Простая supervised/RL gate на синтетическом ряде, сравнить с fixed-threshold | кандидат в ядро |
| I-007 | **DATA + LIVENESS + CHECKPOINT protocol** | Разделить содержательные события, heartbeat и полную ресинхронизацию; heartbeat может нести hash/ID anchor | Молчание должно означать «изменений нет», а не «датчик умер» | Lightweight state-synchronization protocol для sparse/event-driven sources | Heartbeat/liveness protocols; AoI | AD (аналогия с Manchester/NRZI), совместная формализация | 4 | 4 | Может оказаться инженерной деталью, а не научным результатом | Прототип UDP/MQTT: dropped packets, drift, recovery, anchor hash | вспомогательная |
| I-008 | **Age of Incorrect / Useful Information** | Оценивать не просто возраст последнего пакета, а насколько устаревшее состояние уже стало неверным/опасным для задачи | Позволяет редкие heartbeat/update без бессмысленной периодики | Task-aware age metric, возможно совместно с latent error/invariants | Age of Information; Age of Incorrect Information | совместно | 4 | 4 | Поле уже развито; нужна специфичная метрика/задача | Сравнить fixed heartbeat, AoI и task-aware AoII на одной динамической системе | гипотеза |
| I-009 | **Value-of-Information triggering** | `send iff expected benefit of update > communication/compute cost` | Универсальная постановка значимости вместо ручного порога | VoI для latent/micro-agent state + multiple update modes | Value of Information in remote estimation/control | совместно | 5 | 5 | Базовый принцип уже известен | Построить cost function и сравнить threshold vs learned VoI policy | гипотеза |
| I-010 | **Edge micro-agents / SLM latent communication** | Малые модели на edge поддерживают локальное состояние и получают не полный контекст, а редкие task-relevant latent updates | Экономия bandwidth, RAM/KV, энергии и inference | Совместная оптимизация communication + memory + inference при сохранении task quality | Agentic edge intelligence; task-oriented agent communication; split inference | AD связал идею с SLM/edge | 5 | 5 | Очень быстро меняющаяся область, легко уйти в 1.2.1/телеком | Два micro-agent процесса на CPU-only: full-context vs latent/event updates | кандидат в ядро |
| I-011 | **Минимальная информация для эквивалентного решения** | Минимизировать `bits(update)` при условии, что решение малой модели эквивалентно решению при полном состоянии | Теоретическое ядро task-aware representation | Rate/quality formulation для decision-preserving state representation | Information bottleneck; task-oriented communication | совместно | 5 | 5 | Может потребовать сложной теории, чтобы не остаться эвристикой | Классификационная toy-задача: найти rate–decision-error curve | гипотеза |
| I-012 | **N-body как метрологический benchmark** | Использовать астродинамику не как предмет новизны, а как контролируемую динамическую систему с известными инвариантами | Возвращает старый домен без необходимости снова делать вклад в астрофизику | Benchmark methodology: compression/latent updates оцениваются по энергии, импульсу, long-horizon drift | Symplectic/N-body integration; structure-preserving methods | совместно | 5 | 5 | Нужно аккуратно отделить ошибки интегратора от ошибок representation | Простая N-body система: raw/FLLC/lossy/latent; energy+momentum+trajectory drift | эксперимент |
| I-013 | **SPH как второй benchmark + learned refinement** | SPH дает локальные взаимодействия и неоднородную значимость областей; отдельно возможно ML-based split/merge/refinement | Проверка переносимости метода на другой класс динамики | Learned error/refinement estimator, сохраняющий физические ограничения | Adaptive SPH; learned mesh/particle refinement | AD | 5 | 4 | Потребует повторного погружения в CFD; может размыть диссертацию | Сначала использовать готовый SPH benchmark только как тест, без новой CFD-методики | отложена/benchmark |
| I-014 | **Adaptive multi-agent orchestration by compact state** | Оркестратор выбирает agent/model/task/context по компактному состоянию системы и бюджету | Связывает существующую систему задач для агентов с диссертацией | Политика оркестрации по latent state; trade-off quality/cost/latency/reliability | Multi-agent orchestration; resource-aware scheduling | AD + совместная формализация | 5 | 4 | Может стать слишком продуктовой/инженерной темой | Выбрать один routing decision и сравнить heuristics vs learned policy | гипотеза |
| I-015 | **State-conditioned threshold authorization** | Доли секрета/ключа становятся полезными только когда независимые агенты доказали достижение заданных состояний | Распределенная работа со скрытым контентом; безопасность | Связать threshold secret sharing с verifiable state predicates/attestation | Shamir secret sharing; VSS; MPC; attestation | AD | 2 | 4 | Уходит в 1.2.4/криптографию; нужны security proofs | Сделать threat model и определить, что именно считается доказуемым state predicate | отдельная ветка |
| I-016 | **Молчание как информационный символ** | Отсутствие DATA означает «существенного события нет» только при доказанной liveness и общей модели состояния | Концептуальная основа event-driven protocol | Формализация семантики silence + liveness + confidence/age | Event-triggered systems; timing channels; AoI/AoII | совместно | 4 | 4 | Может быть формулировкой, а не отдельной новизной | Формально задать state machine протокола и failure modes | вспомогательная |

## Ключевые литературные опоры

1. **Distributed Event-Triggered Estimation Over Sensor Networks: A Survey** — IEEE Transactions on Cybernetics, DOI: 10.1109/TCYB.2019.2917179  
   https://pubmed.ncbi.nlm.nih.gov/31199279/

2. **Dynamic Event-triggered Control and Estimation: A Survey** — Machine Intelligence Research, 2021  
   https://link.springer.com/article/10.1007/s11633-021-1306-z

3. **Minimizing the Age of Incorrect Information for Real-time Tracking of Markov Remote Sources** — IEEE ISIT 2021  
   https://ieeexplore.ieee.org/document/9518209/

4. **Towards reasoning-empowered task-oriented communication for agent networks** — npj Wireless Technology, 2026  
   https://www.nature.com/articles/s44459-026-00028-z

5. **A survey on AI-empowered task-oriented sensing, communication, and computation in 6G networks** — Computer Science Review, 2026  
   https://www.sciencedirect.com/science/article/pii/S1574013726000080

6. **Communication-efficient agentic edge intelligence: A survey of federated multi-agent information fusion for LLM-driven edge AI** — Information Fusion, 2026  
   DOI: 10.1016/j.inffus.2026.104577

7. **A survey on Deep Learning in Edge–Cloud Collaboration: Model partitioning, privacy preservation, and prospects** — Knowledge-Based Systems / Elsevier, 2025  
   https://www.sciencedirect.com/science/article/pii/S0950705125000139

8. **On latent dynamics learning in nonlinear reduced order modeling** — Neural Networks, 2025  
   DOI: 10.1016/j.neunet.2025.107146  
   https://www.sciencedirect.com/science/article/pii/S0893608025000255

## Правила ведения

1. Любую новую содержательную идею сначала заносить отдельной строкой, не пытаясь сразу слить ее с существующими.
2. Если идея является развитием другой — сохранять новый ID и указывать связь в формулировке/контексте.
3. Не повышать оценку перспективности только из-за субъективной привлекательности идеи: учитывать prior art, соответствие 1.2.2, экспериментальную проверяемость и путь к публикации.
4. Для каждой идеи по возможности фиксировать **самый дешевый эксперимент, который может ее подтвердить или убить**.
5. По мере изучения литературы добавлять не просто ссылки, а короткий комментарий: что уже сделано и где остается потенциальное окно новизны.
6. Идеи не удалять. Для неудачных менять статус на `отбракована` и кратко фиксировать причину — это предотвращает повторное изобретение уже отвергнутой ветки.
7. Отдельно различать:
   - `ядро кандидатской`;
   - `положение на защиту`;
   - `глава/эксперимент`;
   - `программная инфраструктура`;
   - `отдельная статья/студенческая тема`;
   - `отложенная идея`.
8. При появлении результатов reverse-engineering защищенных диссертаций обновить поля соответствия 1.2.2, риска и перспективности на основании эмпирических данных.

## Текущая рабочая гипотеза ядра

Наиболее сильная объединяющая линия на текущем этапе:

> **Адаптивное представление и синхронизация состояния динамических/распределенных систем, при котором передается не полное состояние, а минимальная task-relevant innovation, достаточная для сохранения требуемых инвариантов, динамики или качества решения при ограниченных ресурсах.**

Текущий условный pipeline:

`shared anchor → local prediction → innovation → significance gate → ignore / latent correction / exact correction / checkpoint → downstream decision`

Эта формулировка пока является **гипотезой направления**, а не утвержденной темой диссертации.