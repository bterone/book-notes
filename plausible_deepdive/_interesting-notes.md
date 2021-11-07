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


They also make use of setups within test descriptions to modify the context and pass it in to tests within the same describe block

```elixir
  describe "POST /register/invitation/:invitation_id" do
    setup do
      inviter = insert(:user)
      site = insert(:site, members: [inviter])

      invitation =
        insert(:invitation,
          site_id: site.id,
          inviter: inviter,
          email: "user@email.co",
          role: :admin
        )

      {:ok, %{site: site, invitation: invitation}}
    end

    test "registering sends an activation link", %{conn: conn, invitation: invitation} do
      post(conn, "/register/invitation/#{invitation.invitation_id}",
        user: %{
          name: "Jane Doe",
          email: "user@example.com",
          password: "very-secret",
          password_confirmation: "very-secret"
        }
      )

      assert_delivered_email_matches(%{to: [{_, user_email}], subject: subject})
      assert user_email == "user@example.com"
      assert subject =~ "is your Plausible email verification code"
    end
  end
```

Keeps tests even more descriptive and precise. Follows Behavior Driven Development / Testing more closely due to setup acting as contexts.

They seem to be using an HTTP interface to connect to their Elixir app using a clickhouse database driver.
Clickhouse seems to be a high performance DB system for real time analytics using SQL.
