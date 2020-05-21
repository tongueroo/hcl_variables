# HclVariables

Parse HCL Variables files. The scope of this library is to only handle `variables.tf` file.

## Usage

```ruby
require "hcl_variables"
code =<<EOL
variable "project" {
  description = "The name of the GCP Project"
  default     = "test"
  type        = "string"
}
variable "name_prefix" {
  type        = "string"
}
EOL

parser = HclVariables::Parser.new(code)
parser.load
# Returns =>
#
# {"variable"=>
#   {"project"=>
#     {"description"=>"The name of project",
#      "default"=>"test",
#      "type"=>"string"},
#    "name_prefix"=>{"type"=>"string"}}}
```

## Installation

```ruby
gem 'hcl_variables'
```

## Notes

* Tried a few different Ruby HCL parsers: [hcl-checker](https://github.com/mfcastellani/hcl-checker), [hcl-rb](https://github.com/Ruin0x11/hcl-rb), [rhcl](https://github.com/winebarrel/rhcl), [ruby-hcl](https://github.com/sikula/ruby-hcl). They all seem to have one issues or another.
* This library preprocesses the text fed to the parser to workaround the parser issues. It's a workaround.
* Able to handle simple variable types and most complex types.
* Not able to handle multi-line complex variable types. There's a spec to document this.
* Will have to fix one of these parsers or write a new one.
* Open to PRs to help.
