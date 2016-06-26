# md-ruby-eval

    Usage: #{$0} [options] --auto
           #{$0} [options] INPUT_FILE OUTPUT_FILE

Evaluates Ruby examples in MD files.

It looks for code blocks starting with '```ruby'. The blocks are evaluated in same order
as they appear in the markdown file. Each top_level parseable piece of code is evaluated
and the value is added as a comment, e.g.:

    # Title

    First evaluated block:

    ```ruby
    a = 1 + 2
    def a; :a; end #
    [a,
     :b]
    ```

    Continuing in next block

    ```ruby
    a
    ```

becomes

    # Title

    First evaluated block:

    ```ruby
    a = 1 + 2         # => 3
    def a; :a; end
    [a,
     :b]              # => [:a,:b]
    ```

    Continuing in next block

    ```ruby
    a                 # => 3
    ```

A parseable piece of code ended with '#' will be evaluated but it's result is not
added to the output as a comment, which is useful for method and class definitions.
