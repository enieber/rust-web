---
theme:
  name: tokyonight-night
title: "Rust para camada web"
sub_title: Do cklick ao processamento
author: Enieber Cunha
---


Agenda
==============

<!-- column_layout: [2, 1] -->

<!-- column: 0 -->

- Bases para rust web
- Camada Web - Do click ao processamento
- Lidando com banco de dados
- Frameworks
<!-- column: 1 -->

<!-- reset_layout -->
<!-- end_slide -->


Sobre Mim
=====================

<!-- column_layout: [2, 1] -->

<!-- column: 0 -->

- Enieber Cunha
- Dev e Ops Fullstack
- Pai em tempo integral



<!-- reset_layout -->


<!-- end_slide -->


## Bases para rust web

- Crates
- Rust Async Await (https://www.youtube.com/watch?v=L0CMkCeAWck)
- Trunk - frontend com webassembly
- runtime-async (tokio/smol)

<!-- end_slide -->

## Camada Web - Do click ao processamneto

- html
- ajax
- http
- middlewares
- banco de dados

<!-- end_slide -->

### HTML - SPA

- leptos (fullstack)

```rust +line_numbers
#[component]
pub fn Button() -> impl IntoView {
  let (count, set_count) = signal(0);
  view! { 
    <button on:click=move |_| { 
        set_count.update(|n| *n += 1);
      }
    >
      "Click me: "
      {count}
    </button>
  }
}
```

<!-- end_slide -->


- dioxus (react like - WA - multiplatform)

```rust +line_numbers
use dioxus::prelude::*;

pub fn App() -> Element {
    let mut count = use_signal(|| 0);

    rsx! {
        h1 { "High-Five counter: {count}" }
        button { onclick: move |_| count += 1, "Up high!" }
        button { onclick: move |_| count -= 1, "Down low!" }
    }
}
```
<!-- end_slide -->

- Yew  (html like - WA)
```rust +line_numbers
use yew::prelude::*;

#[component]
fn App() -> Html {
    let counter = use_state(|| 0);
    let onclick = {
        let counter = counter.clone();
        move |_| {
            let value = *counter + 1;
            counter.set(value);
        }
    };

    html! {
        <div>
            <button {onclick}>{ "+1" }</button>
            <p>{ *counter }</p>
        </div>
    }
}

fn main() {
    yew::Renderer::<App>::new().render();
}
```
<!-- end_slide -->

- sycamore (DSL - WA)

```rust +line_numbers
use sycamore::prelude::*;

#[component]
fn Counter(initial: i32) -> View {
    let mut value = create_signal(initial);

    view! {
        button(on:click=move |_| value += 1) {
            "Count: " (value)
        }
    }
}
```
<!-- end_slide -->

- topcoat (nextjs like)

```rust +line_numbers
use topcoat::{
    Result,
    context::Cx,
    router::{module_router, page},
    view::{View, component, view},
};

#[tokio::main]
async fn main() {
    topcoat::start(module_router!().build()).await.unwrap();
}

#[page]
async fn home(cx: &Cx) -> Result<impl View> {
    Ok(view! {
        <!DOCTYPE html>
        <html>
            <body>
                hello(name: "World")
            </body>
        </html>
    })
}

#[component]
async fn hello(cx: &Cx, name: &str) -> Result<impl View> {
    Ok(view! { <h1>"Hello, " (name) "!"</h1> })
}

```
<!-- end_slide -->

### HTML - template

- Tera (runtime verify - based in Jinja2)
- Askama (Compile time verify - based in Jinja2)
- outros 

<!-- end_slide -->

### Ajax

- reqwest (with feature json)
- Datastar (SSE stream)

<!-- end_slide -->

### HTTP

- axum (ergonomics and modularity)
- poem (full-featured and easy-to-use web)
- actix (powerful, pragmatic, and extremely fast web framework for Rust)
- salvo (Simple yet powerful web framework)
- warp (super-easy, composable, web server framework for warp speeds)
- dropshot (expose REST APIs from a Rust program)

<!-- end_slide -->

## Bancos de dados

Para lidar com diferentes bancos de dados para web, existe alguns padrões como uso de DSL com ORMs ou acesso direto ao banco.

<!-- end_slide -->

### ORM

- diesel (sync orm)
- sea-orm (async orm)

<!-- end_slide -->

### Acesso direto ao banco

- sqlx (sql toolkit)
- rust-postgres (acesso ao postgres)
- mysql (acesso ao mysql)

<!-- end_slide -->

## Bancos reescritos em rust

- pg-rust (running in browser)
- turso (sqlite with replica)

<!-- end_slide -->

## Frameworks Web

- loco.rs (The one-person framework: axum + sea-orm + tera)
- doido (Built on convention over configuration: Based in loco.rs build by HUEHUE-BR - Fabiano Martins)
- summer.rs (Application framework written in rust inspired by java's spring-boot)
- blixt (Lightning-fast Rust web framework: axum + sqlx + askama)

<!-- end_slide -->



### Tanks

- Mastodon (https://bolha.us/@enieber)
- Github (https://github.com/enieber)
- Site (https://profile-enieber.vercel.app/)

<!-- end_slide -->

## References

- https://github.com/oxidecomputer/dropshot
- https://github.com/seanmonstar/reqwest
- https://data-star.dev/
- https://salvo.rs/
- https://github.com/seanmonstar/warp
- https://github.com/poem-web/poem
- https://actix.rs/
- https://www.sea-ql.org/SeaORM/
- https://diesel.rs/
- https://github.com/transact-rs/sqlx
- https://trunk-rs.github.io/trunk/
- https://sycamore.dev/
- https://leptos.dev/
- https://yew.rs/
- https://loco.rs/
- https://doido-rs.github.io/
- https://summer-rs.github.io/
- https://ripkitten-co.github.io/blixt/
- https://github.com/enieber/encurta-ai
- https://github.com/enieber/hello_rullst
- https://github.com/enieber/actix_web
- https://github.com/enieber/hello-primavera
