# Azure-Networking Samples

# To add a Security Rule
```Java
$HomeNsg = Get-AzNetworkSecurityGroup -Name nsgEast -ResourceGroupName "connectivityEast"
$params  = @{
  'Name'                     = 'Home3'
  'NetworkSecurityGroup'     = $HomeNsg
  'Protocol'                 = '*'
  'Direction'                = 'Inbound'
  'Priority'                 = 250
  'SourceAddressPrefix'      = '75.75.75.75'
  'SourcePortRange'          = '*'
  'DestinationAddressPrefix' = 'VirtualNetwork'
  'DestinationPortRange'     = 3389,8080,80,22,139,145,137,138
  'Access'                   = 'Allow'
}
Add-AzNetworkSecurityRuleConfig @params | Set-AzNetworkSecurityGroup
```

# To UPDATE a Security Rule
```Java
$UpdatedIp = "73.75.75.75"
$HomeNsg   = Get-AzNetworkSecurityGroup -Name nsgEast -ResourceGroupName "connectivityEast"
$params    = @{
  'Name'                     = 'Home'
  'NetworkSecurityGroup'     = $HomeNsg
  'Protocol'                 = '*'
  'Direction'                = 'Inbound'
  'Priority'                 = 200
  'SourceAddressPrefix'      = $UpdatedIp
  'SourcePortRange'          = '*'
  'DestinationAddressPrefix' = 'VirtualNetwork'
  'DestinationPortRange'     = 3389,8080,80,22,139,145,137,138
  'Access'                   = 'Allow'
}
Set-AzNetworkSecurityRuleConfig @params | Set-AzNetworkSecurityGroup
```
# To REMOVE a Security Rule
``` Java
 Get-AzNetworkSecurityGroup -Name nsgEast -ResourceGroupName "connectivityEast" | 
    Remove-AzNetworkSecurityRuleConfig -Name 'Home3' | 
    Set-AzNetworkSecurityGroup
```
 
