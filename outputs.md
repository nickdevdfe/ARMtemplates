# Outputs


# for nested

When you next a template, it will be give a name (eg nestedTemplate). 
you can use the 'reference' to pull its output

"value": "[reference('nestedTemplate').outputs.result.value]"