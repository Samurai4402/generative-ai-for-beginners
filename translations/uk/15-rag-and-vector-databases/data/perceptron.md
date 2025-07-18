<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "59021c5f419d3feda19075910a74280a",
  "translation_date": "2025-07-09T17:02:18+00:00",
  "source_file": "15-rag-and-vector-databases/data/perceptron.md",
  "language_code": "uk"
}
-->
# Вступ до нейронних мереж: Перцептрон

Однією з перших спроб реалізувати щось подібне до сучасної нейронної мережі була робота Френка Розенблатта з Cornell Aeronautical Laboratory у 1957 році. Це була апаратна реалізація під назвою "Mark-1", призначена для розпізнавання примітивних геометричних фігур, таких як трикутники, квадрати та кола.

|      |      |
|--------------|-----------|
|<img src='images/Rosenblatt-wikipedia.jpg' alt='Frank Rosenblatt'/> | <img src='images/Mark_I_perceptron_wikipedia.jpg' alt='The Mark 1 Perceptron' />|

> Зображення з Wikipedia

Вхідне зображення представлялося у вигляді масиву з 20x20 фотодіодів, тому нейронна мережа мала 400 входів і один бінарний вихід. Проста мережа містила один нейрон, який також називають **логічним елементом з порогом**. Ваги нейронної мережі діяли як потенціометри, які потрібно було вручну налаштовувати під час фази навчання.

> ✅ Потенціометр — це пристрій, який дозволяє користувачу регулювати опір у колі.

> The New York Times писала про перцептрон у той час: *зародок електронного комп’ютера, який [ВМС] очікують зможе ходити, говорити, бачити, писати, відтворювати себе і усвідомлювати своє існування.*

## Модель перцептрона

Припустимо, у нашій моделі є N ознак, тоді вхідний вектор буде вектором розміру N. Перцептрон — це модель **бінарної класифікації**, тобто він може розрізняти два класи вхідних даних. Ми припустимо, що для кожного вхідного вектора x вихід нашого перцептрона буде або +1, або -1, залежно від класу. Вихід обчислюється за формулою:

y(x) = f(w<sup>T</sup>x)

де f — це ступінчаста функція активації

## Навчання перцептрона

Щоб навчити перцептрон, потрібно знайти вектор ваг w, який класифікує більшість значень правильно, тобто дає найменшу **помилку**. Ця помилка визначається за допомогою **критерію перцептрона** таким чином:

E(w) = -∑w<sup>T</sup>x<sub>i</sub>t<sub>i</sub>

де:

* сума береться по тих навчальних прикладах i, які класифіковані неправильно
* x<sub>i</sub> — вхідні дані, а t<sub>i</sub> — або -1, або +1 для негативних і позитивних прикладів відповідно.

Цей критерій розглядається як функція від ваг w, і нам потрібно її мінімізувати. Часто використовується метод, який називається **градієнтним спуском**, при якому ми починаємо з деяких початкових ваг w<sup>(0)</sup>, а потім на кожному кроці оновлюємо ваги за формулою:

w<sup>(t+1)</sup> = w<sup>(t)</sup> - η∇E(w)

Тут η — так званий **швидкість навчання**, а ∇E(w) позначає **градієнт** функції E. Після обчислення градієнта отримуємо

w<sup>(t+1)</sup> = w<sup>(t)</sup> + ∑ηx<sub>i</sub>t<sub>i</sub>

Алгоритм на Python виглядає так:

```python
def train(positive_examples, negative_examples, num_iterations = 100, eta = 1):

    weights = [0,0,0] # Initialize weights (almost randomly :)
        
    for i in range(num_iterations):
        pos = random.choice(positive_examples)
        neg = random.choice(negative_examples)

        z = np.dot(pos, weights) # compute perceptron output
        if z < 0: # positive example classified as negative
            weights = weights + eta*weights.shape

        z  = np.dot(neg, weights)
        if z >= 0: # negative example classified as positive
            weights = weights - eta*weights.shape

    return weights
```

## Висновок

У цьому уроці ви дізналися про перцептрон, який є моделлю бінарної класифікації, та як навчити його, використовуючи вектор ваг.

## 🚀 Виклик

Якщо хочете спробувати побудувати власний перцептрон, спробуйте цей лабораторний практикум на Microsoft Learn, який використовує Azure ML designer


## Огляд та самостійне вивчення

Щоб побачити, як можна використовувати перцептрон для розв’язання навчальної задачі, а також реальних проблем, і продовжити навчання — перейдіть до Perceptron notebook.

Ось також цікава стаття про перцептрони.

## Завдання

У цьому уроці ми реалізували перцептрон для задачі бінарної класифікації і використали його для розпізнавання двох рукописних цифр. У цій лабораторній роботі вам потрібно повністю розв’язати задачу класифікації цифр, тобто визначити, яка цифра найімовірніше відповідає заданому зображенню.

* Інструкції
* Notebook

**Відмова від відповідальності**:  
Цей документ було перекладено за допомогою сервісу автоматичного перекладу [Co-op Translator](https://github.com/Azure/co-op-translator). Хоча ми прагнемо до точності, будь ласка, майте на увазі, що автоматичні переклади можуть містити помилки або неточності. Оригінальний документ рідною мовою слід вважати авторитетним джерелом. Для критично важливої інформації рекомендується звертатися до професійного людського перекладу. Ми не несемо відповідальності за будь-які непорозуміння або неправильні тлумачення, що виникли внаслідок використання цього перекладу.