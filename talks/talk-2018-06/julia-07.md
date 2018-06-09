# Julia 0.7-alpha

Julia 0.7 is Julia 1.0 but with deprecations.

New features:
- [NEWS.md](https://github.com/JuliaLang/julia/blob/v0.7.0-alpha/NEWS.md)
- nice [blog post](https://white.ucc.asn.au/2018/06/01/Julia-Favourite-New-Things.html)
  by Lyndon White

Main bits:
- Pkg3
- Named Tuples
  - used for faster function keyword-arguments
- Field access overloading [#24960](https://github.com/JuliaLang/julia/pull/24960) (satirical package [OO.jl](https://github.com/mauro3/OO.jl))
- extensible broadcasting [Blog by Matt Bauman](https://julialang.org/blog/2018/05/extensible-broadcast-fusion)
- efficient small unions
  - missing values
  - new iteration interface
- logging features
