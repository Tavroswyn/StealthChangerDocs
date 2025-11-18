## Requirements
Adding more tools increases the power draw. The required wattage for your build will need to be calculated depending on the chosen hardware for each tool by the end user. 

!!! info "Wattage Calculation"
    See the following example of how one could calculate the wattage required for 6 tool heads.

    - Printing heater max output = `70W`
    - Printing fans - 3 total = `(0.1A * 3 fans) * 24V = 7.2W`
    - Resting heater output (30% of max for 5 tools) = `((70W / 100) * 30) * 5 tools = 105W`
    - Resting fans - 5 tools - `(0.1A * 24V) * 5 tools = 12W`
    - Extruder motors - 0.6A for 6 tools - `(0.6A * 24V) * 6 tools = 86W`

    6 tools with a 70w heater has resulted in `280W` total. This greatly exceeds the standard Voron 200W power supply without taking the rest of the system in to account and either an additional power supply is required to make up the difference or the standard power supply needs to be replaced with a larger wattage supply.

!!! danger "Unsure?"
    If you are unsure of your power requirements please reach out for help from the community via one of the social platforms. 
