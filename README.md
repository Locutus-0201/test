```markdown
% COS214 — Final Exam Cheat Sheet (Two‑Column Print)
% Consolidated: EO3 2025, 2024, 2022 + Tut1,2,3,4,5,7,10
% Generated: 2025-11-13

<style>
/* Two-column print styles for pandoc -> PDF via LaTeX or HTML->PDF.
   If converting via pandoc to PDF, the 'columns' variable can be used.
   For HTML->PDF, CSS below will create two columns when printed. */
body { font-family: "DejaVu Sans", Arial, sans-serif; font-size: 10.5pt; line-height: 1.15; }
h1, h2, h3 { color: #0A3D62; }
.container { column-count: 2; column-gap: 28px; }
.block { break-inside: avoid-column; margin-bottom: 12px; padding-bottom: 6px; border-bottom: 1px solid #eee; }
.pattern-title { font-weight: bold; font-size: 10.5pt; color: #1B9CFC; }
.smallcode { font-family: monospace; font-size: 9.5pt; background:#f7f9fb; padding:6px; display:block; white-space:pre-wrap; border-radius:4px; border:1px solid #e6eef8; }
.keywords { background: #f0f8ff; padding:4px 6px; border-radius:4px; font-size:9pt; display:inline-block; margin-top:6px;}
</style>

<div class="container">

# COS214 — Final Exam Cheat Sheet

Purpose:
One place to scan fast during the exam. Each pattern block is the same micro‑format so you can find the right answer in seconds:
Intent • Recognition clues • Participants (exact names to write) • 1–2 sentence exam answer • Pasteable code/line • Quick pitfalls & keywords

How to use:
- Scan the “Recognition” keywords in any question text. If you see one of these phrases, jump to the pattern block and copy the one‑liner + participant mapping into your answer.
- For diagram tasks, open the Diagram Cheat section and follow the exact symbols & minimal objects markers expect.
- For small code completions (Singleton::instance, Factory, Builder, Memento usage), copy the short snippets from the “Pasteable lines” subsection.

---

<div class="block">
<div class="pattern-title">Abstract Factory</div>
- Intent: Provide an interface for creating families of related products.  
- Recognition: factory with createX() methods returning related products.  
- Participants: AbstractFactory, ConcreteFactory(s), AbstractProduct(s), ConcreteProduct(s).  
- One‑liner: "Abstract Factory provides matching product families via factory interface so client code remains independent of concrete products."  
- Paste: <span class="smallcode">auto btn = factory-&gt;createButton(); auto menu = factory-&gt;createMenu();</span>  
- Keywords: <span class="keywords">family of products • createX • matching set</span>
</div>

<div class="block">
<div class="pattern-title">Builder</div>
- Intent: Construct complex objects step‑by‑step via a Director.  
- Recognition: makeX/addX methods and a Director orchestrating calls; getResult().  
- Participants: Director (Renderer), Builder (interface), ConcreteBuilder(s), Product (TextElement/Cake).  
- One‑liner: "Builder separates construction steps from representation; Director calls builder steps in a fixed sequence."  
- Paste: <span class="smallcode">director.construct(builder); auto p = builder.getResult();</span>  
- Tip: use when question mentions "recipe, steps, layered construction".  
</div>

<div class="block">
<div class="pattern-title">Factory Method</div>
- Intent: Let subclasses decide which concrete product to create.  
- Recognition: virtual create() in base; subclass overrides create() to return concrete product.  
- Participants: Creator, ConcreteCreator, Product, ConcreteProduct.  
- One‑liner: "Factory Method defers instantiation to subclasses; use when one-step product creation varies by subclass."  
- Paste: <span class="smallcode">Product* p = creator->create();</span>  
- Keywords: <span class="keywords">virtual create • subclass picks product</span>
</div>

<div class="block">
<div class="pattern-title">Prototype</div>
- Intent: Create objects by cloning a prototypical instance.  
- Recognition: clone()/replicate() or copy constructor usage.  
- Participants: Prototype, ConcretePrototype(s).  
- One‑liner: "Prototype duplicates objects using clone()/replicate() to avoid complex construction."  
- Paste: <span class="smallcode">auto copy = original->replicate();</span>  
</div>

<div class="block">
<div class="pattern-title">Singleton</div>
- Intent: Ensure a single instance and global access.  
- Recognition: static getInstance(), protected/private ctor, deleted copy/assign.  
- Participants: Singleton class.  
- One‑liner: "Singleton controls single instance creation; prevent copy/assign and prefer thread‑safe lazy init."  
- Paste (C++11): <span class="smallcode">template&lt;typename T&gt; T& Singleton&lt;T&gt;::instance(){ static T theInstance; return theInstance; }</span>  
- Pitfalls: watch thread safety and lifetime; use local static (C++11) or smart pointers for more control.
</div>

<!-- structural patterns -->
<div class="block">
<div class="pattern-title">Adapter (class/object)</div>
- Intent: Convert one interface to another.  
- Recognition: Adapter implements Target and uses Adaptee via delegation (object) or inheritance (class).  
- Participants: Target, Adapter, Adaptee.  
- One‑liner: "Adapter translates Adaptee's interface to Target expected by clients."  
- Paste (object adapter): <span class="smallcode">class Adapter : public Target { Adaptee a; void op() override { a.oldOp(); } };</span>  
</div>

<div class="block">
<div class="pattern-title">Bridge</div>
- Intent: Decouple abstraction from implementation.  
- Recognition: Abstraction has Implementor pointer/composition.  
- One‑liner: "Bridge separates abstraction and implementation into parallel hierarchies."  
</div>

<div class="block">
<div class="pattern-title">Composite</div>
- Intent: Part‑whole tree; components and composites share interface.  
- Recognition: Component with add/remove/getChildren; Composite holds a collection of components.  
- One‑liner: "Composite allows treating single objects and compositions uniformly."  
- Tip: composition = filled diamond, aggregation = hollow diamond.
</div>

<div class="block">
<div class="pattern-title">Decorator</div>
- Intent: Add responsibilities at runtime by wrapping objects.  
- Recognition: Decorator implements same interface and holds Component*.  
- One‑liner: "Decorator wraps component to add behaviour; use to extend objects without inheritance explosion."  
- Paste: <span class="smallcode">Component* c = new LoggingDecorator(orig);</span>
</div>

<div class="block">
<div class="pattern-title">Facade</div>
- Intent: Simplify a complex subsystem via a single interface.  
- One‑liner: "Facade provides a unified higher-level interface to a set of subsystems."
</div>

<div class="block">
<div class="pattern-title">Flyweight</div>
- Intent: Share intrinsic state across many fine‑grained objects to save memory.  
- Recognition: factory returns shared objects keyed by intrinsic state.  
- One‑liner: "Flyweight shares immutable parts; extrinsic state is supplied by the client."  
- Paste (cache style): <span class="smallcode">auto f = factory.get(key); f->operation(extrinsic);</span>
</div>

<div class="block">
<div class="pattern-title">Proxy</div>
- Intent: Surrogate to control access to RealSubject.  
- Recognition: Proxy implements same interface and performs checks/lazy/caching.  
- One‑liner: "Proxy controls or augments access to the real object while preserving the same interface."
</div>

<!-- behavioral patterns -->
<div class="block">
<div class="pattern-title">Strategy</div>
- Intent: Encapsulate interchangeable algorithms/policies.  
- Recognition: Context has Strategy pointer and calls strategy->execute(); strategies implement same interface.  
- Participants: Context, Strategy, ConcreteStrategy(s).  
- One‑liner: "Strategy encapsulates an algorithm to be swapped at runtime."  
- Paste (ControlMethod): <span class="smallcode">ControlMethod* remote = new RemoteControl(); Appliance* tv = new TV(remote); tv->turnOn();</span>
</div>

<div class="block">
<div class="pattern-title">State</div>
- Intent: Allow object behavior to vary with internal state.  
- Recognition: Context holds State*, and each State implements behavior and transitions.  
- One‑liner: "State encapsulates state-specific behavior; transitions are owned by states."
</div>

<div class="block">
<div class="pattern-title">Command</div>
- Intent: Encapsulate requests as objects with execute()/undo().  
- One‑liner: "Commands enable queuing, undo/redo and transactional behaviour."
- Paste: <span class="smallcode">for(auto it = executed.rbegin(); it != executed.rend(); ++it) (*it)->undo(receiver);</span>
</div>

<div class="block">
<div class="pattern-title">Memento</div>
- Intent: Snapshot and restore object state.  
- One‑liner: "Memento captures internal state; Caretaker stores snapshots for later restore."
- Paste: <span class="smallcode">auto s = originator->createMemento(); if(error) originator->restore(s);</span>
</div>

<div class="block">
<div class="pattern-title">Observer</div>
- Intent: One‑to‑many automatic notification.  
- Recognition: Subject attach/detach/notify; Observers implement update().  
- One‑liner: "Observer decouples publisher and subscribers."
- Paste (Qt style): <span class="smallcode">connect(checkBox, &QCheckBox::toggled, pushButton, &QPushButton::setEnabled);</span>
</div>

<div class="block">
<div class="pattern-title">Mediator</div>
- Intent: Centralize communications to reduce coupling.  
- One‑liner: "Mediator acts as a hub to coordinate interactions."
</div>

<div class="block">
<div class="pattern-title">Visitor</div>
- Intent: Add operations to object structures without changing nodes.  
- One‑liner: "Visitor allows adding operations (printer, analyzer) by using accept/visit methods."
- Paste: <span class="smallcode">element->accept(printerVisitor);</span>
</div>

<div class="block">
<div class="pattern-title">Interpreter</div>
- Intent: Evaluate expressions using classes for grammar rules.  
- One‑liner: "Interpreter maps grammar symbols to class nodes that interpret context."
</div>

<div class="block">
<div class="pattern-title">Template Method</div>
- Intent: Algorithm skeleton in base class; primitives implemented by subclasses.  
- One‑liner: "Template method defines steps and defers specifics to subclasses."
</div>

<div class="block">
<div class="pattern-title">Iterator</div>
- Intent: Traversal abstraction.  
- One‑liner: "Iterator hides traversal details; check push/pop behavior to determine order (LIFO vs FIFO)."
</div>

<div class="block">
<div class="pattern-title">Chain of Responsibility</div>
- Intent: Pass requests along a chain of handlers.  
- One‑liner: "Chain lets multiple handlers try to process a request in sequence."
</div>

<!-- UI & Tutorial sections -->
<div class="block">
<h2>UI & Event Patterns (quick)</h2>
- Signals/slots -> Observer; Handlers -> Command; QPushButtonState -> State.  
- Paste: <span class="smallcode">handler->setWidget(myButton); handler->doAction();</span>
- QSet/HandlerSet -> Factory Method (makeTool()).
</div>

<div class="block">
<h2>Diagram Cheats (short)</h2>
- Class: inheritance (hollow triangle), composition (filled diamond), aggregation (hollow diamond), multiplicities.  
- Object: show instanceName:Class and attribute values.  
- Sequence: lifelines + activations; owner of method is lifeline with activation.  
- Communication: number messages, show links.  
- Activity: fork/join for threads, decisions diamond.  
- State: states, transitions, guards `[cond]`, entry/exit actions.  
</div>

<div class="block">
<h2>Tools — quick commands</h2>
- Valgrind: <span class="smallcode">valgrind --leak-check=full --show-leak-kinds=all --track-origins=yes ./program</span>  
- gdb: <span class="smallcode">gdb ./program</span> then `break main`, `run`, `next`, `step`, `print var`, `bt`.  
- Doxygen: <span class="smallcode">doxygen -g; edit Doxyfile; doxygen Doxyfile</span>  
- Git: <span class="smallcode">git status; git add .; git commit -m "msg"; git push</span>
</div>

<div class="block">
<h2>Tutorials — high‑value snippets</h2>
<ul>
<li><b>Tut1</b> ShoppingCart Memento + Template: originator = ShoppingCart, memento = CartMemento, caretaker = Customer. Save snapshot before destructive changes: <span class="smallcode">CartMemento* m = cart->createMemento();</span></li>
<li><b>Tut2</b> Beer production: Factory Method in BeerProductionStation::makeBeer(type); Composite: CaseOfBeer (Bottle[24]) → Crate (CaseOfBeer[32]).</li>
<li><b>Tut3</b> CatFest: Prototype for CatDesign::replicate(); Decorator for design add-ons; State for PlatformState (Preparation/Live/Closed).</li>
<li><b>Tut4/Tut5</b> UI: connect/emit => Observer; handlers => Command; QPushButtonState => State. Example: <span class="smallcode">connect(checkBox, &QCheckBox::toggled, pushButton, &QPushButton::setEnabled);</span></li>
<li><b>Tut7</b> ControlMethod -> Strategy sample; code diagnostics: ensure proper instantiation and deletion order, use smart pointers to manage shared ControlMethod instances.</li>
<li><b>Tut10</b> Animal Care: Visitor for operations across animals; Proxy for safe interactions/control layer.</li>
</ul>
</div>

<div class="block">
<h2>Final Decision Checklist (one sweep)</h2>
- "skeleton / steps" → Template Method  
- "choose algorithm at runtime" → Strategy  
- "undo/redo / list of operations" → Command  
- "snapshot / revert to commit" → Memento  
- "multi‑stage construction" → Builder  
- "many identical small objects / memory" → Flyweight  
- "wrap to add behaviour at runtime" → Decorator  
- "translate interface" → Adapter  
- "control access same interface" → Proxy  
- "parse grammar / interpret" → Interpreter  
- "one-to-many notifications" → Observer  
- "part-whole relationships" → Composite  
- "single instance" → Singleton
</div>

</div> <!-- end container -->

```
