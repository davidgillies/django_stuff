Subclass the dashoboard and menu using the given commands to create files:

    python manage.py custommenu
    python manage.py customdashboard
    
These create dashboard.py and menu.py.  Put them into your app and add to the settings.py:

    ADMIN_TOOLS_INDEX_DASHBOARD = 'api_renderer.dashboard.CustomIndexDashboard'
    ADMIN_TOOLS_APP_INDEX_DASHBOARD = 'api_renderer.dashboard.CustomAppIndexDashboard'
    ADMIN_TOOLS_MENU = 'api_renderer.menu.CustomMenu'
    
Add some stuff to CustonIndexDashboard:

        self.children.append(modules.LinkList(
            _('Reports'),
            children=[
                {
                    'title': _('Some Google Chart Reports'),
                    'url': '/admin/somepath',
                    'external': False,
                },
                      ]
        ))

Add some stuff to the CustomMenu:

            items.MenuItem(
                title= _('Reports'), url='#', children=[
                items.MenuItem(title=_('Some Google Chart Reports'), url='/admin/somepath')]
            ),
            
Here adding MenuItems.  

