# usage
```lua
local cheaters = {}

cheaters.list = {}
cheaters.list_temp = {}
cheaters.fetch_link = "https://raw.githubusercontent.com/tihomirocrew/gmod_cheater_list/refs/heads/main/list.json"

function cheaters.fetch_on_success(body, length, headers, code)
    cheaters.list_temp = {}
    cheaters.list_temp = util.JSONToTable(body)
end

function cheaters.fetch_on_failure(msg)
    print(msg)
end

function cheaters.update()
    http.Fetch(cheaters.fetch_link, cheaters.fetch_on_success, cheaters.fetch_on_failure, nil)
    cheaters.list = cheaters.list_temp
end

cheaters.update()

timer.Create("CheatersUpdate", 10, 0, function()
    cheaters.update()
end)
```
