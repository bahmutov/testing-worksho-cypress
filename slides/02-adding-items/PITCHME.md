## ☀️ Part 2: Testy na pridávanie položiek v TodoMVC

### 📚 Naučíš sa

- základné commandy pre prácu s elementami
- zorganizovanie testov pomoco Mocha hookov

+++

- maj `todomvc` aplikáciu zapnutú
- otvor si `cypress/integration/02-adding-items/spec.js` vo svojom editore
- klikni na file `02-adding-items/spec.js` in Cypress

+++

## ⚠️ Todo položky

**Note:** Testy, ktoré budeme spolu písať nie sú urobené tak, aby zresetovali stav aplikácie. Prosím pred spustením testu poodstraňuj todo položky

O tom, ako zresetovať stav aplikácie sa pobavíme neskôr 😉.

Na spúšťanie jednotlivých testov použi `it.only`
+++

```js
it.only('starts with zero items', () => {
  // check if the list is empty initially:
  //   find the selector for the individual TODO items
  //   in the list
  //   use cy.get(...) and it should have length of 0
})
```

**tip** použi `cy.get`, `should('have.length', ...)`

[https://on.cypress.io/get](https://on.cypress.io/get)

+++

```js
it('adds two items', () => {
  // repeat twice
  //    get the input field
  //    type text and "enter"
  //    assert that the new Todo item
  //    has been added added to the list
})
```

**tip** použi `cy.get`, `cy.type`, `cy.contains`, `cy.click`

Note:
Draw distinction between commands and assertions, show how commands can be chained,
each continues to work with the subject of the previous command. Assertions do
not change the subject.

+++

## Refaktoring 1/3

- otvor stránku nanovo pred každým testom

Note:
Avoid duplicate `cy.visit('localhost:3000')` command at the start of each test.

+++

## Refaktoring 2/3

- presuň url do `cypress.json`

**tip** look at [https://on.cypress.io/configuration](https://on.cypress.io/configuration)

+++

## Refaktoring 3/3

- vytvor si pomocnú funkciu 

**tip** všetko je len javascript

Note:
Move `addItem` function into a separate file and import from the spec file. It is just JavaScript, and Cypress bundles each spec file, so utilities can have `cy...` commands too!

+++

## 💡 Pro tips

- zmeň viewport cez `cypress.json`

+++

## Bonus

Unit testy vs. end-to-end testy

### Unit testy

```javascript
import add from './add'
test('add', () => {
  expect(add(2, 3)).toBe(5)
})
```

- arrange - action - assertion

+++

### End-to-end testy

```javascript
const addItem = text => {
  cy.get('.new-todo').type(`${text}{enter}`)
}
it('can mark items as completed', () => {
  const ITEM_SELECTOR = 'li.todo'
  addItem('simple')
  addItem('difficult')
  cy.contains(ITEM_SELECTOR, 'simple').should('exist')
    .find('input[type="checkbox"]').check()
  // have to force click because the button does not appear unless we hover
  cy.contains(ITEM_SELECTOR, 'simple').find('.destroy').click({ force: true })
  cy.contains(ITEM_SELECTOR, 'simple').should('not.exist')
  cy.get(ITEM_SELECTOR).should('have.length', 1)
  cy.contains(ITEM_SELECTOR, 'difficult').should('be.visible')
})
```

- **tip** check out `cy.pause` command

Note:
Revisit the discussion about what kind of tests one should write. E2E tests can cover a lot of features in a single test, and that is a recommended practice. If a test fails, it is easy to debug it, and see how the application looks during each step.

+++

### Unit vs E2E

- ak popisuješ ako funguje kód: unit test
- ak popisuješ ako kód používa user: end-to-end test

+++

Štruktúra foldrov a test filov

```text
cypress/integration/
  featureA/
    first-spec.js
    second-spec.js
  featureB/
    another-spec.js
    errors-spec.js
```

+++

Štruktúra vo vnútri test filov pomocou Mocha funkcii

```js
describe('Feature A', () => {
  beforeEach(() => {})

  it('works', () => {})

  it('handles error', () => {})

  // context is alias of describe
  context('in special case', () => {
    it('starts correctly', () => {})

    it('works', () => {})
  })
})
```
