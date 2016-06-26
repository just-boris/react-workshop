---

layout: ribbon

style: |

    #Cover h2 {
        margin:30px 0 0;
        color:#FFF;
        text-align:center;
        font-size:70px;
        }
    #Cover p {
        margin:10px 0 0;
        text-align:center;
        color:#FFF;
        font-style:italic;
        font-size:20px;
        }
        #Cover p a {
            color:#FFF;
            }
    #Picture h2 {
        color:#FFF;
        }
    #SeeMore h2 {
        font-size:100px
        }
    #SeeMore img {
        width:0.72em;
        height:0.72em;
        }
---

# React workshop {#Cover}

## The plan

1. React comparing with other frameworks
2. Popular recipies


## Component frameworks

1. React
2. Angular
3. WebComponents (Polymer)

And more

## Components to build web applications

Screenshot CASI

## We need to go deeper

Screenshot components inside components

## Components are actually custom HTML-tags

    var MyApp = React.createClass({
        render() {
            return <div>
                <LoginForm /> // <-- this is component
                <footer>Copyright 2016, bla-bla-bla</footer> // <-- this is just html-tag
            </div>
        }
    })

## Why not Backbone?

    var MyApp = Marionette.LayoutView.extend({
        regions: {
            login: '.login' // do not forget to add this class into template!
        },
        onRender() {
            this.login.show(new LoginForm())
        }
    })

## How to implement this?

    <div>
        <Offer data={data} />
        <Sidebar state="open">
            <Journal data={data} />
        </Sidebar>
    </div>

## Why not Angular

```
    <ul>
        <li *ngFor="#item in items" (click)="onClick">{{item}}</li>
    </ul>
```

There is a special new syntax, that you have to learn


## What is JSX?

This is JavaScript extension, which allows you to embed HMTL

    var html = <div>My test content</div>

Actually it will be a function call

    var html = React.createElement('div', 'My test content')

## JSX

Javascript is now your template engine

    <ul>
        {items.map(item => {
            return <li>{item.title}: {item.value}</li>
        })}
    </ul>

## Virtual DOM

    * Re-renders only that parts, that have been changed
    * Detects and evaluate your custom components as well as usual html-tags
    * Easy to listen to events

# Recipies

## Read and set input value

    var Form = React.createClass({

        onChange(event) {
            this.setState({
                value: event.target.value
            });
        },

        render() {
            return <input name="firstName" value={this.state.value} onChange={this.onChange}>;
        }
    });

## Routing

    <Router>
        <IndexRoute component={IndexPage} />
        <Route path="/account/:id" component={AccountPage} />
    </Router>

## Share values between components

Use Redux:

    ComponentA = connect(state => {value: state.value})(ComponentA)

    ComponentB = connect(state => {value: state.value})(ComponentB)

## Global store object

Picture of store workflow

## How to do ajax

Use Axios - modern Ajax library based on promises.

Server requests should happen in "actions"

    var saveAction = function(data) {
        return function(dispatch) {
            axios.post('/api/endpoint', data).then(function() {
                dispatch({type: 'SAVE_SUCCESS'})
            })
        }
    }

## A note about functional programming

Use can write React components as functions

    function AccountInfo(account) {
       return <div>
            <div className="column">
                <p>Name: {account.name}</p>
                <p>Last name: {account.lastName}</p>
            </div>
            <div className="column">
                <p>Amount: {account.creditAmount}</p>
                <p>Duration: {account.duration}</p>
            </div>
       </div>
    }

## Summary

    * You have a state - just render it. Don't care about previous state
    * If you want to do something, emit an action
    * Keep your components as simple as possible
