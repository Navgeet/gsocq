With the current schema, a codeq consists of:
- :codeq/file
- :codeq/loc
- :codeq/parent
- :codeq/code
- attr (:clj/def, :clj/use, ...)
- deftype (def, defn, ...)

A sample codeq:

```clj
;; clojure.tools.analyzer>
(-> (ast (defn foo [x]
           (first x)))
    clojure.pprint/pprint)

{:codeq/file 100001
 :codeq/code 100002
 :codeq/ast 100003
 :codeq/infer 100004}

;; entity 100002
{:code/sha "foo"
 :code/text "(defn foo [x]
               (first x))"}

;; entity 100003
{:ast/op :def
 :ast/env <some-id>
 :ast/var #<Var@121b0d8: #<analyzer$foo clojure.tools.analyzer$foo@8d8fce>>
 :ast/meta <some-id>
 :ast/init 100005
 :ast/init-provided true
 :ast/is-dynamic false}

;; entity 100005
{:ast/op :fn-expr
 :ast/env <some-id>
 :ast/methods [100006]
 :ast/variadic-method nil
 :ast/tag nil}

;; entity 100006
{:ast/op :fn-method
 :ast/env <some-id>
 :ast/body 100007
 :ast/required-params [100012]
 :ast/rest-param nil}

;; entity 100007
{:ast/op :do
 :ast/env <some-id>
 :ast/exprs [100008]}

;; entity 100008
{:ast/op :invoke
 :ast/env <some-id>
 :ast/protocol-on nil,
 :ast/is-protocol false,
 :ast/args [100009]
 :ast/fexpr 100010
 :ast/is-direct false
 :ast/site-index -1
 :ast/tag nil}

;; entity 100009
{:ast/op :local-binding-expr
 :ast/env <some-id>
 :ast/local-binding 100011
 :ast/tag nil}

;; entity 100011
{:ast/op :local-binding
 :ast/env <some-id>
 :ast/sym x
 :ast/tag nil
 :ast/init nil}

;; entity 100010
{:ast/op :var
 :ast/env <some-id>
 :ast/var #<Var@1d71441: #<core$first clojure.core$first@8e9e3d>>
 :ast/tag nil}

;; entity 100012
{:ast/op :local-binding
 :ast/env <some-id>
 :ast/sym x
 :ast/tag nil
 :ast/init nil}
```

Every ast op node will be associated with a `:codeq/code` node
containing the corresponding form.
