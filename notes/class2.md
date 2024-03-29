# Working with Files

Already saw the current filename variable `__FILE__` - Ruby has two classes that make working with files easier: `Dir` and `File`

## Dir

```ruby
Dir.pwd
Dir.home
Dir.chdir "bin"
Dir.chdir ".."
Dir.entries "examples"
Dir.glob "**/*.rb"
=> ["examples/example1.rb"]
Dir.mkdir "silly"
Dir.entries "."
Dir.rmdir "silly"
```

## File

```ruby
File.exist?("Gemfile")
=> true
File.basename("Gemfile.lock")
=> "Gemfile.lock"
File.realpath("Gemfile")
=> "/Users/mmorga/Box Sync/Classes/Ruby/Gemfile"
File.basename(File.realpath("Gemfile"))
=> "Gemfile"
=> "/Users/mmorga/Box Sync/Classes/Ruby/Gemfile"
File.dirname(File.realdirpath("Gemfile"))
=> "/Users/mmorga/Box Sync/Classes/Ruby"
File.dirname("Gemfile")
=> "."
```

### Reading a file

Lots of ways to do this:

```ruby
f = File.read("Gemfile")
=> "source \"https://rubygems.org\"\n\ngroup :development, :test do\n  gem \"pry\"\n  gem \"rubocop\"\n  gem \"minitest\"\n  gem \"minitest-context\"\n  gem \"minitest-colorize\"\n  gem \"minitest-documentation\"\n  gem \"guard\"\n  gem \"guard-minitest\"\n  gem \"guard-bundler\"\n  gem \"guard-rubocop\"\nend\n\ngroup :test do\n  gem \"simplecov\", require: false\nend\n"
f = File.readlines("Gemfile")
=> ["source \"https://rubygems.org\"\n",
 "\n",
 "group :development, :test do\n",
 "  gem \"pry\"\n",
 "  gem \"rubocop\"\n",
 "  gem \"minitest\"\n",
 "  gem \"minitest-context\"\n",
 "  gem \"minitest-colorize\"\n",
 "  gem \"minitest-documentation\"\n",
 "  gem \"guard\"\n",
 "  gem \"guard-minitest\"\n",
 "  gem \"guard-bundler\"\n",
 "  gem \"guard-rubocop\"\n",
 "end\n",
 "\n",
 "group :test do\n",
 "  gem \"simplecov\", require: false\n",
 "end\n"]
source "https://rubygems.org"

group :development, :test do
  gem "pry"
  gem "rubocop"
  gem "minitest"
  gem "minitest-context"
  gem "minitest-colorize"
  gem "minitest-documentation"
  gem "guard"
  gem "guard-minitest"
  gem "guard-bundler"
  gem "guard-rubocop"
end

group :test do
  gem "simplecov", require: false
end
```

### Common File Types like CSV and YAML

Ruby has classes to make it easier to read YAML and CSV files.

```ruby
require 'csv'
=> true
[138] pry(main)> CSV.foreach("data/RaisedBedGardenCosts.csv") do |line|
[138] pry(main)*   puts line.inspect
[138] pry(main)* end
[nil, nil, nil, "Option 1", nil, nil, nil, nil, "Option 2", nil, nil, nil, nil, "Option 3", nil, nil, nil, nil]
["Number", "Length", "Dimension", "Description", "Length", "Cost Per", "# Pieces", "Total", "Description", "Length", "Cost Per", "# Pieces", "Total", "Description", "Length", "Cost Per", "# Pieces", "Total"]
["Posts", nil, nil, "Cedar", nil, nil, nil, nil, "Cedar", nil, nil, nil, nil, "Pine", nil, nil, nil, nil]
["5", "27", "4x4", nil, "96", "$16.45", "1.41", "$23.13", nil, "96", "$16.45", "1.41", "$23.13", nil, "96", "$9.95", "1.41", "$13.99"]
["Sub Total", nil, nil, nil, nil, nil, nil, "$23.13", nil, nil, nil, nil, "$23.13", nil, nil, nil, nil, "$13.99"]
[nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil]
["Sides:", nil, nil, "Cedar 5/4\"", nil, nil, nil, nil, "Cedar 2\"", nil, nil, nil, nil, "Pine 2\"", nil, nil, nil, nil]
["4", "48", "? X 6", nil, "144", "$11.97", "1.33", "$15.96", nil, "96", "$12.55", "2.00", "$25.10", nil, "144", "$7.87", "1.33", "$10.49"]
["4", "72", "? X 6", nil, "144", "$11.97", "2.00", "$23.94", nil, "96", "$12.55", "3.00", "$37.65", nil, "144", "$7.87", "2.00", "$15.74"]
["4", "60", "? X 6", nil, "144", "$11.97", "1.67", "$19.95", nil, "96", "$12.55", "2.50", "$31.38", nil, "144", "$7.87", "1.67", "$13.12"]
["4", "36", "? X 6", nil, "144", "$11.97", "1.00", "$11.97", nil, "96", "$12.55", "1.50", "$18.83", nil, "144", "$7.87", "1.00", "$7.87"]
["4", "12", "? X 6", nil, "144", "$11.97", "0.33", "$3.99", nil, "96", "$12.55", "0.50", "$6.28", nil, "144", "$7.87", "0.33", "$2.62"]
["Sub Total", nil, nil, nil, nil, nil, nil, "$75.81", nil, nil, nil, nil, "$119.23", nil, nil, nil, nil, "$49.84"]
[nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil]
["Top:", nil, nil, "Cedar 5/4\"", nil, nil, nil, nil, "Cedar 5/4\"", nil, nil, nil, nil, "Pine 2\"", nil, nil, nil, nil]
["1", "48", "? X 6", nil, "144", "$11.97", "0.33", "$3.99", nil, "144", "$11.97", "0.33", "$3.99", nil, "144", "$7.87", "0.33", "$2.62"]
["1", "72", "? X 6", nil, "144", "$11.97", "0.50", "$5.99", nil, "144", "$11.97", "0.50", "$5.99", nil, "144", "$7.87", "0.50", "$3.94"]
["1", "60", "? X 6", nil, "144", "$11.97", "0.42", "$4.99", nil, "144", "$11.97", "0.42", "$4.99", nil, "144", "$7.87", "0.42", "$3.28"]
["1", "36", "? X 6", nil, "144", "$11.97", "0.25", "$2.99", nil, "144", "$11.97", "0.25", "$2.99", nil, "144", "$7.87", "0.25", "$1.97"]
["1", "12", "? X 6", nil, "144", "$11.97", "0.08", "$1.00", nil, "144", "$11.97", "0.08", "$1.00", nil, "144", "$7.87", "0.08", "$0.66"]
["Sub Total", nil, nil, nil, nil, nil, nil, "$18.95", nil, nil, nil, nil, "$18.95", nil, nil, nil, nil, "$12.46"]
[nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil, nil]
["Grand Total", nil, nil, nil, nil, nil, nil, "$117.90", nil, nil, nil, nil, "$161.31", nil, nil, nil, nil, "$76.30"]
["For Four", nil, nil, nil, nil, nil, nil, "$471.58", nil, nil, nil, nil, "$645.24", nil, nil, nil, nil, "$305.19"]
=> nil
```

### YAML

```ruby
y = YAML.parse_file("data/yaml.yml").to_ruby
=> {"YAML"=>"YAML Ain't Markup Language",
 "What It Is"=>"YAML is a human friendly data serialization standard for all programming languages.",
 "YAML Resources"=>
  {"YAML 1.2 (3rd Edition)"=>"http://yaml.org/spec/1.2/spec.html",
   "YAML 1.1 (2nd Edition)"=>"http://yaml.org/spec/1.1/",
   "YAML 1.0 (1st Edition)"=>"http://yaml.org/spec/1.0/",
   "YAML Issues Page"=>"https://github.com/yaml/yaml/issues",
   "YAML Mailing List"=>"yaml-core@lists.sourceforge.net",
   "YAML IRC Channel"=>"#yaml on irc.freenode.net",
   "YAML Cookbook (Ruby)"=>"http://yaml4r.sourceforge.net/cookbook/ (local)",
   "YAML Reference Parser"=>"http://yaml.org/ypaste/"},
 "Projects"=>
  {"C/C++ Libraries"=>["libyaml", "Syck", "yaml-cpp"],
   "Ruby"=>["psych", "RbYaml", "yaml4r"],
   "Python"=>["PyYaml", "PySyck"],
   "Java"=>["JvYaml", "SnakeYAML", "YamlBeans", "JYaml"],
   "Perl Modules"=>["YAML", "YAML::XS", "YAML::Syck", "YAML::Tiny", "PlYaml"],
   "C#/.NET"=>["yaml-net", "yatools.net"],
   "PHP"=>["php-yaml", "syck", "spyc"],
   "OCaml"=>["ocaml-syck"],
   "Javascript"=>["JS-YAML", "JS-YAML Online# Browserified JS-YAML demo, to play with YAML in your browser."],
   "Actionscript"=>["as3yaml"],
   "Haskell"=>["YamlReference"],
   "Others"=>["yamlvim (src)"]},
 "Related Projects"=>["Rx", "Kwalify", "yaml_vim", "yatools.net", "JSON", "Pygments"],
 ...
```

# Decision Making in Ruby

```ruby
if fruit.first == "Apple"
  puts "Yep, it's an apple alright"
end

if fruit.first == "Pear"
  puts "Yep, it's an pear alright"
elsif fruit.second == "Pear"
  puts "Second!"
else
  puts "I don't know what this is."
end

unless fruit.first == "Apple"
  puts "I said I want an apple!"
end

something = 10
while something < 100
  puts "not yet"
  something = something + 10
end
puts "ok #{something} == 100"

puts "Apple!" if fruit.first == "Apple"

# nil is a special Object in Ruby
nothing = nil
if nothing.nil?
  puts "Yep nothing is nil"
end

# same result
unless nothing
  puts "Yep nothing is still nil"
end
```

# Time for something real

Here's a little program to write. Take a CSV file in and transform it into an HTML table.

Here's a table in HTML:

```html
<table>
  <tr>
    <th>col1</th>
    <th>col2</th>
    <th>col3</th>
  </tr>
  <tr>
    <td>cell1</td>
    <td>cell2</td>
    <td>cell3</td>
  </tr>
</table>
```

So how would you do this:

```ruby
puts "<table>"
CSV.foreach("data/RaisedBedGardenCosts.csv") do |line|
  puts "<tr>"
  line.each do |cell|
    puts "<td>#{cell}</td>"
  end
  puts "</tr>"
end
puts "</table>"
```

