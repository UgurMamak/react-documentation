# React Dokümantasyon

- [DOM](#DOM)
- [Virtual DOM](#Virtual-DOM) 
- [One-Way Binding  ve Two-Way Binding](One-Way-binding-ve-Two-Way-Binding)
- [Create React App](#Create-React-App)
- [Propslar](#Propslar)
	- [PropTypes](#PropTypes)
- [Eventler](#Events)
- [State'ler](#State'ler )
  - [Statefull ve stateless componentler](#Statefull-ve-Statelesss-Componentler)
- [Lifecycle (Yaşam Döngüsü)](#Lifecycle)
  - [Initialization](#Initialization)
    - [constructor](#Initialization)
  - [Mounting](#Mounting)
	- [componentWillMount](#componentWillMount)
	-  [componentDidMount](#componentDidMount)
  - [Updation](#Updation)
	 -  [componentWillReceiveProps](#componentWillReceiveProps)
	 -  [ShouldcomponentUpdate](#shouldComponentUpdate)
	 - [ComponentWillUpdate](#componentWillUpdate)
	 - [ComponentDidUpdate](#componentDidUpdate)
- [Fetching](#Fetching)
- [React Router](#React-Router)
    - [Link](#Link )
	- [Redirect](#Redirect) 
	- [Switch](#switch)
- [High Order Component](#High-Order-Component)
- [Pure component](#Pure-Component)
- [Redux](#Redux)
  - [Action](#Action)
  - [Reducer](#Reducer)
  - [Store](#Store)
  - [Merge Props](#Merge-props)
  - [Redux Thunk Middleware](#Redux-Thunk-Middleware)
  - [AsyncAwait-Yapısı-ile-Servis-Çağrımı](#AsyncAwait-Yapısı-ile-Servis-Çağrımı)
  - [Immutable Mutable](#Immutable-Mutable)
  - [Immutable Array](#Immutable-Array)
  - [Redux Logger Middleware](#Redux-Logger-Middleware)
  - [Async Action Pattern](#Async-Action-Patterns)
  - [Async Actions Pattern Redux Promise Middleware](#Redux-Promise-Middleware)
- [NOTLAR](#NOTLAR)
- [Kısaltmalar](#Kısaltmalar)
- [#Kaynakça](#Kaynakça)







## DOM
 DOM web sayfalarının bize görünmesini sağlayan HTML elemanlarının hiyerarşik bir biçimde bir arada bulunması anlamına gelen W3C standardıdır [1].
 
 DOM dokümandaki nesnelere erişmek ve içeriğini, stilini, yapısını değiştirmek için kullanılır [1].
 
 DOM, HTML ile programlama dilleri arasında bir **standart** oluşturarak bu dillerin HTML den bilgi alıp, bilgi vermesine yardımcı olur. **DOM**, Nesneler ve özelliklerden oluşur [2].

> DOM**’da **HTML** ile hazırladığınız sayfa, **_belge_**; bu belgenin içine yerleştirdiğiniz her türlü öğe ise **_nesne_** olarak adlandırılır [2].
 
**DOM** da nesnelerin birer öğe (_element_) olarak kullanılabilmesi için hiyerarşik bir düzen izlenerek çağrılmaları gerekir.  HTML’deki her bir elamanın birbiri ile hiyearşik bir yapı oluşturması ile oluşur [2].


![alt text](https://github.com/UgurMamak/react-documentation/blob/master/images/1.png)

![alt text](https://github.com/UgurMamak/react-documentation/blob/master/images/2.png)

https://webmaster.kitchen/dom-document-object-model-nedir/



**DOM** bir ağaç dizini gibi bütün dokümanları birbirine bağlar. Birden fazla programlama dilleri destekler(_JS, PHP, Java, ASP vb._) ve aynı zamanda dosya oluşturmak, elementleri ve içeriklerini silme/ekleme gibi fonsiyonları vardır [2].

## Virtual DOM
Virtual Dom ise Dom yapısının key=>value şeklinde memory'de bulunmuş haline denir. Yani Dom'un kopyasını almak gibi düşünebiliriz.

Örneğin: HTML web saayfası üzerinde herhangi bir değişiklik gerçekleşirse değişikliğin ekrana yansıması için bütün DOM taranır. Yani bütün Dom render edilir.

Virtual Dom'da ise herhangi bir güncelleme ve değişiklik olduğunda ilk önce virtual dom üzerinde yani bellekte yapılır. Daha sonra VDom'dan gerçek dom'a aktarılırken VDOM ve DOM arasındaki farklılıklar kontrol edilir ve sadece farklılığın olduğu yerler kontrol edilir.

## One-Way Binding  ve Two-Way Binding

**one-way binding** 
değişkenlerin ve değerlerin view tarafına aktarımıdır. React'ta JSX tarafında kullandığımız **{variable}**  syntax ‘ı buna en güzel örnektir[3].

    import React from  'react';
    class  App extends  React.Component  {
	    state  = {
	    data:  'Hello word'
	    };
    render(){
	   return  (
	   <div>
		   <p>The data is  =>  {this.state.data}</p>
	  </div>
	  );}}
	  export default  App;

**two-way binding**

![alt text](https://github.com/UgurMamak/react-documentation/blob/master/images/3.jpg)

View tarafına aktarılan data arka taraftanda dinlenmektedir. data<=>view olayına denir [3].

![alt text](https://github.com/UgurMamak/react-documentation/blob/master/images/4.png)


## Create React App
React kullanıcı arayüzü oluşturmak için kullanılan js kütüphanesidir. Framework değildir. View katmanına odaklanır.

    npm install -g create-react-app (react pc'ye kurulumu sağlar)
    npx create-react-app project-name (proje isimlendirme küçük harf olmak zorunda)
    npm start (uygulamayı başlatır.)

## Propslar
props: Bir componentten farklı bir componente aktarılan data'ya props denir. Props read only'dir yani üzerinde değişiklik yapılamaz sadece okunabilirdir.

state:bir componentin kendisine ait olan data'larına state denir.

> NOT: propslar tekrar render edilemezler. Bir kere renderlanırlar. Eğer
> güncellemek istiyorsak state kullanmalıyız.

### PropTypes
Componente gelen propsların içeriklerini, özelliklerini belirlememize yarar.

> import PropTypes from "prop-types" //kullanılan js dosyasında import edilir.

     //gönderilen propların tipini belirlemek için kullanabiliriz.
     //render'dan önce yazılır. 
     static propTypes={ 	
    	    news:PropTypes.array,  
    		name:PropTypes.string}

   Component dışında aşağıdaki şekilde kullanılır. 

    News.propTypes={ //News component ismi
      name:PropTypes.string
     }

    name:PropTypes.string.isRequired //string olsun ve boş olmasın anlamına gelir.
    
    //oneOfType Birden fazla tipi desteklemeyi sağlar.
    name:PropTypes.oneOfType([
    PropTypes.number,
    PropsTypes.string
    ]).isRequired
    
    //shape gelen props object ise gelen objeyi şekillendirmek için kullanılır.
    newData:PropTypes.shape({
    	title:PropTypes.string,
    	desc:PropTypes.string
    })
    
    //static default props eğer belirlenen componentler gelmez ise varsayılan değer vermek için kullanabiliriz.
    static defaultProps={
    	name:"Uğur" //eğer name props'u boş gelirse props'a "Uğur" değeri atanmış olur.
    }





## Events
Context Binding İşlemi

    // 1.yöntem
    constructor(){
    	super();
    	this.addButton=this.addButton.bind(this);
	}
    addButton(){}
	{this.addButton} //JSX'te çağırma şekli
    
    // 2.yöntem
    addButton(){}
	  {this.addButton.bind(this))} //JSX'te çağırma şekli
    
    NOT:Facebook 1.yöntemi tavsiye etmektedir.
    
**Arrow function ile binding işlemi**

    // 1.yöntem
    addButton=()=>{} //arrow function
    {this.addButton} //JSX'te çağırma şekli
    
    // 2.yöntem JSX içinde elementte arrow function tanımlama aşağıdaki gibi yapılmaktadır.
    addButton(){}
    {()=>this.addButton()} //JSX'te çağırma şekli

## State'ler 
Uygulama içinde dataları tutan js objesidir. Her state değişikliğinde component render edilmektedir.

    // React'ın 16.versiyon öncesinde constructor içinde tanımlama yapılıyordu.
    constructor(){
        super();
        this.state={
    	    name:"Uğur"
    	    }
    	}
    //16.versiyon ile birlikte constructor dışında da state tanımlaması yapılabilmektedir.	
    state={
	    name:"Uğur"
    }
    
    //State güncelleme işlemi
    this.setState({name:"Mamak"}) 

### Statefull ve Statelesss Componentler

**Statefull comp.’’ler constructor’da başlatılan bir state’e sahiptir.** statefull component denilen, kendi içinde state tanımı mevcut olan componentin her state'i değiştiğinde componentin **render** fonksiyonunun tekrardan çalışmasını sağlar.

Statefull ve stateless component arasındaki fark birinde state olması diğerinde olmamasıdır. Statefull componentler değişen stateleri takip ederken, stateless componentler kendilerine verilen props aracılığıyla yazdırır veya her zaman aynı şeyi yazdırır yani render işlemi olmaz [7].

![stateful component örn](https://github.com/UgurMamak/react-documentation/blob/master/images/5.png)

![stateless component örn](https://github.com/UgurMamak/react-documentation/blob/master/images/6.png)

Görselde Stateless component bir function olarak yazılmıştır. Bileşenleri olabildiğince basit ve stateless hale getirmeliyiz.

**Bir Bileşeni statefull veya stateless yazacağımıza nasıl karar veriririz?**
Bilgilerin dinamik olarak değişeceği componente ihtiyaç duyuyorsak statefull olmalı.

Bilgi tamamen durağansa ve hiç değişmeyeceğini biliyorsak bu componenti presentational component şeklinde yazmak daha mantıklı olur [7].


![stateless component örn](https://github.com/UgurMamak/react-documentation/blob/master/images/7.png)

setState işlemi tamamlandıktan sonra çalışacak fonksiyon aşağıdaki şekilde yazılabilir.

	this.setState({
	    someState: obj
	}, () => {
	    this.afterSetStateFinished();
	});



## Lifecycle

![stateless component örn](https://github.com/UgurMamak/react-documentation/blob/master/images/8.png)

 ### Initialization
 constructor kısmını ifade eder.  Initial state'ler bind işlemleri tanımlanır. constructor bir kere çalışır.

### Mounting
DOM yaratılınca, insert işlemleri gerçekleşince çağrılan metodlardır.
#### componentWillMount
render'dan önce tetiklenir. (VDOM'dan DOM'a akratım gerçekleşmeden önce çalışır) State değişimi yapılmaz hızlı çalışması gereken işlemler burada yapılabilir. 

> NOT: Update geldiği için kullanılması önerilmiyor.

#### componentDidMount
render işleminden sonra çalışır.
setState işlemleri, servis çağrıları,  Redux bağlantısı apiye bağlanma gibi işlemler burada yapılabilir. 

### Updation
Bir componentin state veya props'unun update edilmesiyle tekrardan render edilmesi sonucu çağrılan methodlardır.
#### componentWillReceiveProps
Child component'e geçtiğimiz props üzerinde değişiklik olursa child component'te cwrp çalışır.

    componentWillReceiveProps(nextProps){//değişen props'u parametre olarak alır.
    
    } 

> NOT: CWRP çalışınca child component tekrar render edilir,.

#### shouldComponentUpdate

 - Componentin render edilip edilmeyeceğini belirtebiliriz. 
 -   Component içinde state veya props değişikliği olduğunda SCU ile kontrol edebiliriz.
 - True veya false döner.  **True dönerse render edilir**. **False dönerse render edilmez**.
 -  False döndüğü zaman CWU’ya girmez.
 
.

     ShouldComponentUpdate(nextProps,nextState){  
            nextState.variable , nextProps.variable //
        	    return true or false
            }

#### componentWillUpdate

    componentWillUpdate(nextProps,nextState){}


#### componentDidUpdate
State veya props değişikliğinde çalışır. bir önceki state ve props değerlerine ulaşabiliriz. 
Hali hazırdaki props değeri ile bir önceki props’u karşılaştırmak için idealdir.

    componentDidUpdate(prevProps,prevState){}

## Fetching
Javascript'in fonksiyonudur. Api'ye bağlanarak data çekme işlemleri yapılabilir. 

    fetch('url')
    	.then(data=>data.json) //data'nın tipini belirledik.
    	.then(a=>{setState({array:a})}) //gelen data array state'ine atanmış olur.
    	
**Axios**
fetching kütüphanesidir.  https://github.com/axios/axios

    axios.get("url")
    	.then(x=>x.data)
        	.then(//atama işlemlerini yapabiliriz.)
    	
   

> NOT: Jquery'de de fetching işlemleri yapılabilmektedir.   
> https://api.jquery.com/jquery.get/   
> https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch


## React Router
https://github.com/ReactTraining/react-router/tree/master/packages/react-router-dom
https://github.com/ReactTraining/react-router/tree/master/packages/react-router
https://github.com/omergulcicek/react-router

npm i react-router
npm i react-router

       import  {  BrowserRouter  as  Router,  Route,  Link,  NavLink,  Redirect,  Switch  }  from  'react-router-dom';
        <BrowserRouter>
            <Route path="/" exact component={App}> //exact Boolean değerdir. Path'in doğruluğuna bakar.
              <Route path="about" component={About} strict /> //strict belli bir yapıya zorlamak anlamına gelir. path'in tam olarak eşleşmesi gerekir.
               <Route path="contact" render={()=>{return (<div></div>)}}/>
              <Route path="inbox" component={Inbox}>
                <Route path="messages/:id" component={Message} /> /inbox/messages (şeklinde path oluşur.)
              </Route>
            </Route>
          </BrowserRouter>

  <br/>
  
    <Route path="/category/:id" component={Category} />
    //match.params.id ile path'deki id değerine ulaşabiliriz.
    const Category=(varaibles)=>{}
    const Category=({match})=>{
    }
   <br/>
   
### Link 

    <Link to="/">
    <Link to="/inbox">
    <Link to="/category/3"> //parametreli kullanımı

   ### NavLink
Link ile aynı işlevi vardır tek farkı navlink style alabilmektedir. Link style alamaz.

    <NavLink to="/" exact activeStyle={{color:"green";}} >AnaSayfa</NavLink> //activeStyle yerine activeClassName kullanarak style yazılabilir.

### Redirect 
Yönlendirme yapmak için kullanılır.
  

      <Route path="/profile" exact strict render={ () => (
        this.state.loggedIn ? ( <Profile/>) : (<Redirect to="/" />)
        )} />
### switch
Konumla eşleşen ilk `<Route>` veya `<Redirect>` childını oluşturur.

    <Switch>
      <Route exact path="/" component={Home}/>
      <Route path="/about" component={About}/>
      <Route path="/:user" component={User}/>
      <Route component={NoMatch}/>
    </Switch>
## High Order Component
React'ta tekrar edilen yapıların tek bir yerden yönetilmesini sağlayan ileri düzey bir tekniktir. Bazı componentler ortak özellik veya fonksiyon vermek istersek, örneği loading kullanmak istiyorsak HOC yazarak istediğimiz componente loading işlemini ekleyebiliriz.
İşlemleri tek bir yerden kontrol etmemizi sağlar. Generic bir yapı oluşturmamızı sağlar.


    import React, {Component} from 'react';
    const LoaderHOC = (WrappedComponent,field) => {
    	return class LoaderHOC extends Component{
    		render(){
    			return  this.props[field].length  ===  0 ? <div>Loading...</div> : <WrappedComponent  {...this.props} />
    		}
    	}
    };
    export default LoaderHOC;
    //HOC örnek
<br>

    import React, {Component} from 'react';
    import LoaderHOC from './LoaderHOC';
    class Posts extends Component {
	    render() {
		    return (
			    <div>{
				 this.props.posts.map(post =>
				    <div key={post.id}>{ post.title }</div>
				    )}
				</div>
				);
		}
    }
    export default LoaderHOC(Posts,'posts');
    Postss.js

## Pure Component
SCU yöntemini kullanması dışında component ile aynıdır. Bizim yerimize SCU yöntemini çalıştırır. shouldComponentUpdate nextState ve nextProps göre bileşenin önceki değerlerine göre değişip değişmediğini algılayıp burda **_forceUpdate_** olup olmayacağına karar vermeye çalışabilir. PureComponent türeyen bileşenlerde ise bu işlem **shallowly compares** ile kendisi karar verir. Ekstra kod yazmanız gerekmez [8]. 

> NOT pure component'i her yerde kullanmamalıyız. shallowly compares işlemi maaliyetlidir. Pure component proje içerisinde stratejik noktalarda kullanılırsa avantajlıdır.

    import React, {PureComponent} from 'react';
        class Posts extends PureComponent {
    	    render() {
    		    return (
    			    <div>{  this.props.secondNumber  }</div>
    				);
    		}
        }
        export default  Posts 
        
## Redux
State yönetimini sağlayan  js kütüphanesidir.
Redux ile **component drilling (component hiyerarşisi)** olayı ortadan kalkar.
Redux belli bir noktaya kadar state geçmişini tutmaktadır.

     <script src="https://unpkg.com/redux@latest/dist/redux.min.js"></script>

> npm install redux 
> npm install react-redux //kullandığın library'e göre değişkenlik gösterir.


![alt text](https://github.com/UgurMamak/react-documentation/blob/master/images/9.png)
### Action
Action’lar uygulama içerisinden store’a iletilen değişkenlerin bilgilerini tutarlar. `dispatch(action)`fonksiyonu ile store’a yazılırlar.  Actionlar js nesneleridir ve içerisinde **type ve payload** tutarlar.  type bilgisi değişken adı gibi, store yazılacak verinin tipini belirler (neyi güncellemesi gerektiğini adlandırır). payload ile de değişmesi gereken veriyi taşır [9].

    {
      type: "YAZI_EKLE",
      baslik: "Redux ile Uygulamalarınızın State'ini Yönetin"
    }
    //action örneği
Uygulama büyüdükçe çok fazla action ortaya çıkacağı için type ifadelerini sabit değişkene atamakta yarar var.

    export const actionTypes = {
	    GET_POSTDETAIL_SUCCESS,
    };
    
    //Action Creators 
    //Action üreten fonksiyonlardır. Bu fonksiyonlar tanımlanan bir action’ı return eder.
    function getPostDetailSuccess(postDetail) {
	    return { 
		    type: actionTypes.GET_POSTDETAIL_SUCCESS, 
		    payload: postDetail
		 };
    }
    
    export  function  getPostDetail(postId) {
	    return  function (dispatch) { 
			axios.get(url).then((result) => {
				dispatch(getPostDetailSuccess(result.data)); //store action dispatch etmek için kullanılır. 
			})
		};
	}

`dispatch()` fonksiyonuna, store nesnesi üzerinden **store.dispatch()** şeklinde kullanımı ile direkt olarak erişilebilir. Fakat React uygulamalarında daha optimize render işlemleri için react-redux kütüphanesinin sunduğu **connect()** yardımcı fonksiyonu kullanılır. Çoklu action üreticilerinin tek seferde dispatch edilmesi için ise **bindActionCreators()** metodundan yararlanılabilir [9].

### Reducer
**State yönetimini sağlar.** Reduce'lar store'a gelen action sonucunda uygulamanın hangi state'inin değişeceğini ve nasıl değiştirileceğini belirler.  Action’dan gelen verileri süzgeçleyip store’da belirtilen veriyi güncellememizi sağlayan bir araç [9]. 
Reducer temel olarak bir JavaScript fonksiyonudur ve önceki state ile action’ı alarak sonraki state’i üretir [9].

Reducer fonksiyonu, pure fonksiyon olmalıdır (Pure fonksiyonlar aynı input için aynı output değeri üreten fonksiyonlardır ve kendi scope’u dışındaki bir değişkene erişmezler ve bu değişkeni değiştirmezler.)

Reducer içerisinde yapılmaması gerekenler:
-   Parametre olarak geçilen argümanlar değiştirilmemelidir.
-   API çağrıları veya sayfa geçişleri gibi yan etki yapan işlemler gerçekleştirilmemelidir.
-   `Date.now()` veya `Math.random()` gibi pure olmayan fonksiyonlar çağrılmamalıdır.  
    Temel olarak bir reducer pure olması gerektiği için sadece hesaplama yapılan işlemleri içermelidir. API çağrımı gibi işlemler reducer’ın sorumluluğu değildir [9].
    
<br/>


    import { actionTypes } from  "./postActions";
    
    const  initialState = {
	    postDetail: [],
    };
    
    export  default  function  PostListReducer(state = initialState, action) { //action yerine {type, payload} şeklinde yazabiliriz. (ES6) ile birlikte kullanılmaya başlandı.
	    switch (action.type) {
		    case  actionTypes.GET_POSTDETAIL_SUCCESS:
			    return {
				    ...state,
					postDetail:  action.payload
			    };
			    
		    case  actionTypes.GET_POSTDETAIL_UNSUCCESS:
			    return {
				    ...state,
				    postDetail:  action.payload,
			    };
		    default:
			    return  state;
		}
    }

> NOT:
>  return { ...state, postDetail: action.payload } kısmında  return
> Object.assign({}, state, {postDetail: action.payload }) şeklinde de
> state değerlerini değiştirebiliriz.
> 
> State’in direkt olarak **değişmemesi**  gerektiği. Reducer’ın pure kalması için `Object.assign()`ile state’in bir kopyası oluşturuldu. Eğer `Object.assign(state, { {postDetail: action.payload  })` şeklinde kullanırsak state’i yine değiştirmiş oluruz. Bu nedenle ilk parametre olarak boş bir nesne `{}` atamamız önemlidir. Eğer Babel gibi bir transpiler kullanıyorsak, nesne yayma operatörünü object spread operator(...state) kullanabiliriz[9].


 
      yazilar: [{title: "title1",}, { title: 'title2',}]

	 case YAZI_EKLE:
          return Object.assign({}, state, {
            yazilar: [ //yazılar nesnesine, eski oluşturulmuş yazılar nesnesi ve action'dan gelen yazı nesnesinin yeni parametreleri ekleniyor.
              ...state.yazilar,
              {
                title: action.title,
              }
            ]
          })


#### combineReducers 
Ayrı ayrı yazılmış olan reducer fonksiyonlarını tek bir çatı altına toplar.

    import {combineReducers} from "redux";
    import PostListReducer from "./post/PostListReducer"
    import DeletePostReducer from "./post/DeletePostReducer"
    const  rootReducer  =  combineReducers({
	    PostListReducer,
	    DeletePostReducer 
    });
    export default rootReducer;

### Store
 Actionlar state'ler üzerinde "Ne yapılacağını", reducerlar ise action'ları temel alarak ilgili state'in "Nasıl güncelleceğini" belirtirken, Store nesnesi ise bu iki elemanı bir araya getirecek bir yapı oluşturur [9]. Store'un sorumlulukları:
-   Uygulama state’inin tutulması,
-   `getState()` metodu ile state’e erişim sağlaması,
-   `dispatch(action)` metodu ile state’in güncellemesini sağlaması,
-   `subscribe(listener)` metodu ile listener’ları bağlaması,
-   `subscribe(listener)` metodundan dönen listener’ları çıkarmasıdır.

Uygulamada tek bir store bulunur. Uygulamada combineReducers() fonksiyonu çağıran a reducer `createStore()` fonksiyonuna parametre olarak geçilebilir:

    import {createStore} from "redux";
    import rootReducer from "./index"
    export default function configureStore(){
	    return createStore(rootReducer)
    }
    const store = createStore(rootReducer)  //bu şekilde de atama yapılabilir.


**React içinde Redux kullanımı**

     //index.js dosyasında store projeye dahil edilir.
    import { Provider } from "react-redux";
    import configureStore from "./redux/configureStore";
    const  store  =  configureStore();
    
    ReactDOM.render(
	    <Provider store={store}>
		    <App />
	    </Provider>,
	    document.getElementById("root")
    );
   
<br>

    //PostDetail.js
    import { connect } from "react-redux";
    import { bindActionCreators } from "redux";
    import * as postActions from "../../redux/post/postActions";
    class  PostDetail  extends  Component  {
    funk(){
	    //this.props.dispatch(actionFunct.("variable")) bu şekilde de action dispatch edileblir.
    }
	    render(){
		    return(
			    <div></div>
		    )
    }};
    
    //const mapStateToProps=state=>{}
    //const mapStateToProps=(state,props)=>{return {...state, myCount:props.count+2}}
    
    function mapStateToProps(state) {//store'daki state'leri props olarak component içerisinde kullanabilmek için yazılır.
	    return {
		    postReducer: state.PostListReducer,//state değerleri postReducer kullanılarak component içinde kullanılabilir.
	    };
    }
    
    /*const mapDispatchToProps={
	    getData:getDAtaAction
    }*/
    
    function mapDispatchToProps(dispatch) {
	    return {
		    actions: {
			    getPost: bindActionCreators(postActions.getPostDetail, dispatch), //action çalışarak reducer tetikler.
		    },
	    }
    }
    
   

    export default connect(mapStateToProps, mapDispatchToProps)(PostDetail); //connect componenti store'a bağlama işlemini gerçekleştirir.

### Merge props

     //hangi props'un nerden geldiğini öğrenebiliriz.
        const mergeProps=(propsFromState,propsFromDispatch,ownProps)=>{
    	    //propsFromState:state'den gelen propsları ifade eder.
    	    //propsFromDispatch:Dispatch'den gelen props'ları ifade eder.
    	    //ownProps:parent comp'tan gelen propslar
    	    return {}
        }
        export default connect(mapStateToProps, mapDispatchToProps,mergeProps)(PostDetail);

Componentler store'u dinler ve değişiklik olduğunda componentler render işlemlerini gerçekleştirebiliyorlar.

#### Redux'ı library veya framework olmadan kullanma şekli 
[Devnot (Redux ile ilgili detatalı bilgi için incele) ](http://devnot.com/2018/redux-nedir/) 

    function rootReducer(state, action){
    	if(action.type==="changeState"){
    		return action.payload.newState
    	} 
    	return state;
    }
    
    
    const store =createStore(rootReducer);
    
    store.getState(); //state'i getirir.
    
    const action={
    	type:"changeState",
    	payload:{
    		newState:"my new State"
    	}
    };
    
    store.dispatch(action); //action'u tetikleyerek reducer'ın state değerini update eder.
    
    store.subscribe(()=>{ ///store'da değişiklik olduğunda haberdar olmak için kullanabiliriz.
		console.log("Store güncellendi",store.getState());
	});  


    

![alt text](https://github.com/UgurMamak/react-documentation/blob/master/images/10.png)

Kısaca anlatmak gerekirse
View katmanında action tetiklenir. (Button gibi)
Action view'den gelen state'i store dispatch eder. (dispatch: action'daki datayı store' a göndermek anlamına gelir.)
Reducer, store'dan güncellenecek state'i alır ve action'dan gelen type ve payload!a göre  değişikliği gerçekleştirir. Daha sonra tekrar store'a gönderir.
Reducerlar pure function'dır yani etkisi yoktur tek bir veri dönerler.

### Redux Thunk Middleware
middleware: ara katman anlamına gelir. Asıl iş yapılmadan önce bu ara katmanda farklı bir iş yapılır sonra asıl iş gerçekleştirilir. 

 Servis çağrıları yapıp istek attığımızda isteğin ne zaman biteceği belli olmuyor. Async işlemler olduğunda middleware kullanarak async işlemi middleware'a veriyoruz işlem tamamlandığında middleware bize cevap dönüyor bizde kullanabiliyoruz. 
 Kısaca async işlemleri middleware kullanarak reducer gibi yapılarımızın pure kalmasını sağlıyoruz.

>  npm install redux-thunk --save

createStore yaratırken redux-thunk eklenmeli

    import {compose,createStore,applyMiddleware} from "redux";
    
    import rootReducer from "./index"
    
    import thunk from "redux-thunk"
    const allEnhancers=compose(
    applyMiddleware(thunk),
    window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__() //redux web tool kullanmak için eklenebilir.
    );
    export default function configureStore(){
    
    return createStore(rootReducer, allEnhancers)
     }

### AsyncAwait Yapısı ile Servis Çağrımı
   Normal kullanım

    export function getUsers(){
    	return dispatch => {
    		axios.get('url')
    			.then(response=>response.data)
    			.then(response=>dispatch(updateUser ( response.name )))
    			.catch(error=>dispatch(showError))
    	}
    }
    
Async await ile kullanım

    export function getUsers(){
	    return async dispatch => {
		    try{
			    const res = await axios.get("url");
			    dispatch(updateUser(res.data.name));
		    }
		    catch (e) {
			    dispatch(showError());
		    }
	    }
    }

### Immutable Mutable
Objeler ve arrayler referans tiptir. Reducer'da state güncellediğimizde memory'deki alanı tamamının değiştirilmemesi gerekiyor. O anki kopyasını alıp üzerinde değişiklik yapıp ondan sonra return etmemiz gerekiyor.  Bu noktada redux'ta immutable geliştirimi yapmamız gerekiyor. 

    return {
    ...state, //Immutable Mutable sağlar(mevcut state'i kopyalar)
    count: state.count + action.payload
    };
    //...state yerine Object.assign kullanılabilir. Fakat ...state kullanımı daha temizdir.
    // Object.assign({},state, count: state.count + action.payload)
   
   
### Immutable Array
	values:[]
	return {
	    ...state,
	    count: state.count + action.payload,
	    values: [...state.values, action.payload] //array bu şekilde immutable  hale getirilir.
    
    };

### Redux Logger Middleware
Önceki state, act.on ve action sonunda ki aktif state bilgilerini browser'a log olarak basmaya yarar.

    npm install redux-logger --save
<br> Kullanımı 

    import  logger  from  'redux-logger';
    import  applyMiddleware  from  'redux';
    import  thunk  from  'redux-thunk';
    const middleware = applyMiddleware(thunk, logger);
    const store = createStore(reducer, middleware);

### Async Action Patterns
action işleminin başlatıldığını beklediğini ve  hata alma durumlarını action ver reducer'da kullanılması.
Reducer'da olması gereken yapılar aşağıdaki gibi olabilir.
  
    case  "FETCH_USERS_START":
    case  "FETCH_USERS_ERROR":
    case  "RECEIVE_USERS":

### Redux Promise Middleware
Bizim yerimize  action dispatch eder.
[incele](https://github.com/pburtchaell/redux-promise-middleware)
    npm install redux-promise-middleware
import reduxPromiseMiddleware from "redux-promise-middleware";

       const middleware = applyMiddleware(reduxPromiseMiddleware,thunk, logger);
        const store = createStore(reducer, middleware);
        
    //Middleware sayesinde hata kontrolünü yapmamıza gerek kalmadı çünkü promise middleware bizim yerimize error dispatch ediyor. Fakat Reducer'u kendimiz tamamlamalıyız.
    const process = store.dispatch({
    type: "FETCH_USERS",
    payload: axios.get('url').then(res => res.data)
    
    });

## NOTLAR

    package.json = Proje hakkında bilgileri içeren bir dosyadır.
    Kurulumu için aşağıdaki kodu yazmak yeterlidir.
    npm init 
    npm init -y //soruları otomatik olarak geçer.
<br>

	Npm Paket Kurulumu 
	
	npm install <paket adı> -g --save-dev
	
	➫ install :paket indirme komutu  
	➫ -g : global olarak indirme  
	➫ --save-dev : indirilen paketi package.json dosyasına kaydeder. 
	
	indirilen paketler node_modules adındaki klasöre indirilerek projeye dahil edilir.
	
	devDependencies  : — save-dev yazdığımız paketlerin bilgileri burada tutulur. Burada tutulan paketler geliştirme ve test için gereklidir.
	
    dependencies  : — save yazdığımızda ise paketlerin bilgileri burada tutulur. Burada tutulan paketler production için gereklidir.
</br>

    super(props) metodunu kullanarak üst-sınıfın bir nesnesini yaratabilir ve onun değişkenlerine değer atayabilirsiniz.

</br>

    Eğer componente bir değişiklik olmayacaksa class component yazılmamalı (statefull) çünkü class componentler react'ın diff algoritmalarına dahil edilir ve üzerinde işlem yaparak farklılık olup olmadığını kontrol eder.
    Class comp. yerine constant kullanarak arrow function şeklinde tanımlama yapmak daha doğru olur.
</br>

    Pure function:  Pure fonksiyonlar aynı input için aynı output değeri üreten fonksiyonlardır ve kendi scope’u dışındaki bir değişkene erişmezler ve bu değişkeni değiştirmezler.

</br>
</br>
</br>
</br>



## Kısaltmalar
npm : node package manager
js: javascript
dom: document object model
vdom: virtual dom

## Kaynakça
>[1](https://biltektasarim.com/blog/html-dom-nedir).
>[2](https://webmaster.kitchen/dom-document-object-model-nedir/#comment-16207)
>[3](https://www.mobilhanem.com/reactjs-two-way-binding/#:~:text=One%2Dway%20binding%20kulland%C4%B1%C4%9F%C4%B1m%C4%B1z%20model,%C4%B1%20buna%20en%20g%C3%BCzel%20%C3%B6rnektir.)
>[4](https://medium.com/@muratdogan/sen-javascriptin-bir-l%C3%BCtfusun-spread-operat%C3%B6r-extended-version-fa5de70beaeb)
>[5](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
[6](https://developer.mozilla.org/tr/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
[7](https://programmingwithmosh.com/javascript/stateful-stateless-components-react/#:~:text=Stateful%20and%20stateless%20components%20have%20many%20different%20names.&text=The%20literal%20difference%20is%20that,always%20render%20the%20same%20thing.)
[8](https://medium.com/frontend-development-with-js/class-component-function-component-hooks-37140f07e9f9)
[9](http://devnot.com/2018/redux-nedir/)



