## Testing
They use [double](https://github.com/sonerdy/double) instead of mocking modules. It acts as a way to inject dependancies on the fly during tests, and doesn't override module behaviour

```elixir
defmodule Example do
  def process(io \\ IO) do # allow an alternative dependency to be passed
    io.puts("It works without mocking libraries!")
  end
end

defmodule ExampleTest do
  use ExUnit.Case
  import Double

  test "example outputs to console" do
    io_stub = stub(IO,:puts, fn(_msg) -> :ok end)

    Example.process(io_stub) # inject the stub module

    # use built-in ExUnit assert_receive/refute_receive to verify things
    assert_receive({IO, :puts, ["It works without mocking libraries!"]})
  end
end
```

Another intresting note is their use of setup in their controller tests and pass it along within the test context

```elixir
describe "GET /api/stats/main-graph - labels" do
    setup [:create_user, :log_in, :create_site]

    test "shows last 30 days", %{conn: conn, site: site} do
      ...
```
