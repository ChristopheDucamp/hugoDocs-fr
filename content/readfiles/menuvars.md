`.URL`
: string

`.Name`
: string

`.Menu`
: string

`.Identifier`
: string

`.Pre`
: template.HTML

`.Post`
: template.HTML

`.Weight`
: int

`.Parent`
: string

`.Children`
: Menu

Notes que les menus ont aussi les fonctions disponibles suivantes : 

[`.HasChildren`](/functions/haschildren/)
: boolean

Additionally, there are some relevant functions available to menus on a page:

[`.IsMenuCurrent`](/functions/ismenucurrent/)
: (menu string, menuEntry *MenuEntry ) boolean

[`.HasMenuCurrent`](/functions/hasmenucurrent/)
: (menu string, menuEntry *MenuEntry) boolean