# Azure_with_powershell_-_ARM
I am here to give you all the codes which can Automate your Job


# Variables for AD
$clientId = ""
$clientSecret = ""
$tenantId = ""
$subId = ""

# Construct the body for the authentication request
$body = @{
    grant_type = "client_credentials"
    client_id = $clientId
    client_secret = $clientSecret
    resource = "https://management.azure.com/"
}

# Construct the authentication request
$authRequest = Invoke-RestMethod -Method Post -Uri "https://login.microsoftonline.com/$tenantId/oauth2/token" -Body $body

# Get the access token
$accessToken = $authRequest.access_token

# Use the access token to authenticate the request
$headers = @{
    "Authorization" = "Bearer $accessToken"
}

# Make the request to list all resource groups
$resourceGroups = Invoke-RestMethod -Method Get -Uri "https://management.azure.com/subscriptions/$c/resourcegroups?api-version=2019-05-10" -Headers $headers

# Print the resource groups
$resourceGroups.value
