# Dist. Быстрый старт

* [Что такое дист](#)
* [Способы подключения Dist](#)
* [](#)

DIST это один вариантов поставки bem-components. Библиотека в виде дист - это предсобранные файлы, которые можно добавлять в HTML страницы с помощью элементов `<link>` и `<script>`.

Докажем, что это самый быстрый способ попробовать библиотеку в действии. Воспользуемся файлами с CDN.

Создадим вот такую форму:

![](https://github.com/bem-site/bem-method/blob/bem-info-data/articles/quick-start-static/quick-start-static__hello-user.ru.png)

Всего 4 шага:

1. Копируем HTML
2. Добавляем на страницу скрипты и стили
3. Пишем CSS
4. Пишем JS




Способы:

* Подключить файлы с CDN — самый быстрый способ.
* Скачать в виде архива — возможность выбрать нужную версию сборки.
* Самостоятельно собрать файлы из исходного кода — возможность собрать еще не выпущенную версию библиотеки.
* Установить с помощью Bower

> **Важно!** надо где-то сказать, чтобы пользовтаься всеми преимуществами БЭМ-библиотек  - уровнями переопрделения, миксами, сборкой только необходимого и не тянуть в проект все стили и скрипты, воспользуйтесь другими видами поставки bem-components - source или compiled.








modules.define('hello', ['i-bem-dom', 'input', 'button'], function(provide, bemDom, Input, Button) {
  provide(bemDom.declBlock('hello', {
    onSetMod: {
      js: {
        inited: function() {
          this._input = this.findChildBlock(Input);
          this._button = this.findChildBlock(Button);

          this._domEvents().on('submit', function(e) {
            e.preventDefault();
          });
        }
      }
    },

    _onClick: function() {
      this._elem('greeting').domElem.text('Привет, ' + this._input.getVal() + '!');
    },

    onInit: function() {
      this._domEvents('button').on('click', this.prototype._onClick);
    }
  }));
});


<form class="hello">
  <div class="hello__greeting">Привет, !</div>
    <span class="input input_theme_islands input_size_m i-bem" data-bem='{"input":{}}'>
      <span class="input__box">
        <input class="input__control" placeholder="Введите имя" autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false">
      </span>
    </span>
    <script>
    modules.require(['i-bem__dom', 'BEMHTML', 'jquery', 'i-bem__dom_init'], function(BEMDOM, BEMHTML, $, init) {
            var html = BEMHTML.apply({
            {
                block: 'input',
                mods: {
                    theme: 'islands',
                    size: 's'
                },
                placeholder: 'Размер s'
            }
       });
    });
    </script>
  <button class="button button_theme_islands button_size_m button_type_submit button__control i-bem" data-bem='{"button":{}}' role="button" type="submit">
    <span class="button__text">Я отправляю данные</span>
  </button>
  <script>
  modules.require(['i-bem__dom', 'BEMHTML', 'jquery', 'i-bem__dom_init'], function(BEMDOM, BEMHTML, $, init) {
            var html = BEMHTML.apply({
           {
                block: 'button',
                mods: {
                    theme: 'islands',
                    size: 'm',
                    type: 'submit'
                },
                text: 'Я отправляю данные'
            }
        });
    });
  </script>
</form>

.hello {
  color: green;
  padding: 10%;
}

hello__greeting {
  margin-bottom: 12px;
}




JavaScript


modules.define('hello', ['i-bem-dom', 'input', 'button'],
    function(provide, bemDom, Input, Button) {

    provide(bemDom.declBlock('hello', {
        onSetMod: {
            js: {
                inited: function() {
                    this._input = this.findChildBlock(Input);
                }
            }
        },

        _onSubmit: function(e) {
            e.preventDefault();
            this._elem('greeting').domElem.text('Привет, ' + this._input.getVal() + '!');
        }
    }, {
        lazyInit: true,
        onInit: function() {
            this._domEvents().on('submit', this.prototype._onSubmit);
        }
    }));

});

modules.require('i-bem-dom__init', function(init) { init(); });

!!
modules.define('hello', ['i-bem-dom', 'input', 'button'],
    function(provide, bemDom, Input, Button) {

    provide(bemDom.declBlock('hello', {
        onSetMod: {
            js: {
                inited: function() {
                    this._input = this.findChildBlock(Input);
                }
            }
        },

        _onSubmit: function(e) {
            e.preventDefault();
            this._elem('greeting').domElem.text('Привет, ' + this._input.getVal() + '!');
        }
    }, {
        lazyInit: true,
        onInit: function() {
            this._domEvents().on('submit', this.prototype._onSubmit);
        }
    }));

});

 modules.require('i-bem-dom__init', function(init) { init(); });





HTML
<form class="hello i-bem" data-bem='{ "hello": {} }'>
  <div class="hello__greeting">Привет, !</div>
    <span class="input input_theme_islands input_size_m i-bem" data-bem='{"input":{}}'>
      <span class="input__box">
        <input class="input__control" placeholder="Введите имя" autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false">
      </span>
    </span>
  <button class="button button_theme_islands button_size_m button_type_submit button__control i-bem" data-bem='{"button":{}}' role="button" type="submit">
    <span class="button__text">Я отправляю данные</span>
  </button>
</form>



CSS
.hello {
  color: green;
  padding: 10%;
}

.hello__greeting {
  margin-bottom: 12px;
}






