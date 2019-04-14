---
layout: page
title: rdflib.js
subtitle: Using the rdflib.js library in iOS
use-site-title: true
show-avatar: false
---

1. Install the rdflib.js library to your mac from [https://github.com/linkeddata/rdflib.js](https://github.com/linkeddata/rdflib.js) (using npm).

2. Bundle the library with browserify in standalone mode:
```
browserify src/index.js --standalone RDF  > rdfbundle.js
```

3. Standalone mode gives you access to all exports in index.js using RDF.  eg RDF.graph(), RDF.sym(), RDF.parse(), RDF.serialize().

4. Add rdfbundle.js to your iOS project in Xcode.  

5. Import JavaScriptCore into your file.

6. Create a javascript context: 
```swift
var context = JSContext()
``` 

7. Write the rdf bundle into the context: 
```swift
guard let rdfPath = Bundle.main.path(forResource: "rdfbundle", ofType: "js")
    else { print("Unable to read resource files."); return }
do {
    let jsCode = try String(contentsOfFile: rdfPath, encoding: String.Encoding.utf8)
    _ = context?.evaluateScript(jsCode)
}
catch {
    print("Evaluate script failed")
}
```

8. You can now use the rdflib api in your Xcode project, eg:
```swift
context?.evaluateScript("""
    var store = RDF.graph();
    var VCARD = new RDF.Namespace('http://www.w3.org/2006/vcard/ns#');
    var me = store.sym('https://wrmack.inrupt.net/profile/card#me');
    var profile = me.doc();
    store.add(me, VCARD('fn'), 'Warwick McNaughton', profile);
""")
```

9. You can debug running javascript using *Safari - Develop - [your machine] - Automatically show web inspector for JSContexts*

10. See [RDF-iOS](https://github.com/wrmack/RDF-iOS) for example code.