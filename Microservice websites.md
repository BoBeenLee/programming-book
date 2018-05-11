
[Microservice websites](https://www.youtube.com/watch?v=4KVOuQDIfmw)

#### Performance strategy

Simple server-side HTML pages (when applicable) + HTTP/2 => Great page load performance


Frontend teams / services

Teams are self organized
Teams develop, release and test themselves
Teams are operational responsible
Teams own the whole lifecycle of the services they create

Use [ESI](https://www.w3.org/TR/esi-lang) as a base 

Use AJAX transclusion for:
* Personalized content
* Client-side pages and components
* Lazy loading below the fold

How to share CSS (and JS)?
1. Fragment consumers re-implement CSS (high coupling)
2. Common CSS framework (high coupling)
3. Fragment producers export CSS (high cohesion)

Fragment type dependencies


What common dependencies can fragment producers assume?

* CSS reset
* Polyfills
* Basic typography

Technology diversity
[Shared fragments have no dependencies]

Summary

* Simple (and diverse) services => greate per-service performance
* Transclusion: Edge Side Includes ( + AJAX )
	* Style/script resource fragments
* Shared fragments have no dependencies

