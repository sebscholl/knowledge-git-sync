# Django Authentication

Last Edited: December 19, 2019 11:43 PM

# Authentication support is bundled as a Django contrib module in **django.contrib.auth**.

# By default, the required configuration is already included in the **[settings.py](http://settings.py/)**

Necessary Installed Apps:

1. **'django.contrib.auth'** contains the core of the authentication framework, and its default models.2
2. **'django.contrib.contenttypes'** is the Django [content type system](https://docs.djangoproject.com/en/2.0/ref/contrib/contenttypes/), which allows permissions to be associated with models you create.

Necessary Middleware:

1. **[SessionMiddleware](https://docs.djangoproject.com/en/2.0/ref/middleware/#django.contrib.sessions.middleware.SessionMiddleware)** manages [sessions](https://docs.djangoproject.com/en/2.0/topics/http/sessions/) across requests.
2. **[AuthenticationMiddleware](https://docs.djangoproject.com/en/2.0/ref/middleware/#django.contrib.auth.middleware.AuthenticationMiddleware)** associates users with requests using sessions.

### **Creating users[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#creating-users)**

The most direct way to create users is to use the included **[create_user()](https://docs.djangoproject.com/en/2.0/ref/contrib/auth/#django.contrib.auth.models.UserManager.create_user)** helper function:

**>>> from** **django.contrib.auth.models** **import** User

**>>>** user = User.objects.create_user('john', '[lennon@thebeatles.com](mailto:lennon@thebeatles.com)', 'johnpassword')

# At this point, user is a User object that has already been saved

# to the database. You can continue to change its attributes

# if you want to change other fields.

**>>>** user.last_name = 'Lennon'

**>>>** user.save()

### **Changing passwords[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#changing-passwords)**

Django does not store raw (clear text) passwords on the user model, but only a hash (see [documentation of how passwords are managed](https://docs.djangoproject.com/en/2.0/topics/auth/passwords/) for full details).

Change a password programmatically, using **[set_password()](https://docs.djangoproject.com/en/2.0/ref/contrib/auth/#django.contrib.auth.models.User.set_password)**:

**>>> from** **django.contrib.auth.models** **import** User

**>>>** u = User.objects.get(username='john')

**>>>** u.set_password('new password')

**>>>** u.save()

### **Authenticating users[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#authenticating-users)**

**`authenticate`(*request=None*, ***credentials*)[[source]](https://docs.djangoproject.com/en/2.0/_modules/django/contrib/auth/#authenticate)[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.authenticate)**

Use **[authenticate()](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.authenticate)** to verify a set of credentials. It takes credentials as keyword arguments, **username** and **password** for the default case, checks them against each [authentication backend](https://docs.djangoproject.com/en/2.0/topics/auth/customizing/#authentication-backends), and returns a **[User](https://docs.djangoproject.com/en/2.0/ref/contrib/auth/#django.contrib.auth.models.User)** object if the credentials are valid for a backend. If the credentials aren’t valid for any backend or if a backend raises **[PermissionDenied](https://docs.djangoproject.com/en/2.0/ref/exceptions/#django.core.exceptions.PermissionDenied)**, it returns **None**. For example:

**fromdjango.contrib.authimport**authenticate

user=authenticate(username='john', password='secret')

**if** user **is** **not** **None**:

*# A backend authenticated the credentials*

**else**:

*# No backend authenticated the credentials.*

# Rather if you’re looking for a way to login a user, use the **[LoginView](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.views.LoginView)**.

## Permissions and Authorization**[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#permissions-and-authorization)**

Django comes with a simple permissions system. It provides a way to assign permissions to specific users and groups of users.

Permissions can be set not only per type of object, but also per specific object instance. By using the **[has_add_permission()](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/#django.contrib.admin.ModelAdmin.has_add_permission)**, **[has_change_permission()](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/#django.contrib.admin.ModelAdmin.has_change_permission)** and **[has_delete_permission()](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/#django.contrib.admin.ModelAdmin.has_delete_permission)** methods provided by the **[ModelAdmin](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/#django.contrib.admin.ModelAdmin)** class, it is possible to customize permissions for different object instances of the same type.

**# CHECKING PERMISSIONS**

Assuming you have an application with an **[app_label](https://docs.djangoproject.com/en/2.0/ref/models/options/#django.db.models.Options.app_label)** **foo** and a model named **Bar**, to test for basic permissions you should use:

- add: **user.has_perm('foo.add_bar')**
- change: **user.has_perm('foo.change_bar')**
- delete: **user.has_perm('foo.delete_bar')**

### **Programmatically creating permissions[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#programmatically-creating-permissions)**

While [custom permissions](https://docs.djangoproject.com/en/2.0/topics/auth/customizing/#custom-permissions) can be defined within a model’s **Meta** class, you can also create permissions directly. For example, you can create the **can_publish** permission for a **BlogPost** model in **myapp**:

**from** **myapp.models** **import** BlogPost

**from** **django.contrib.auth.models** **import** Permission

**from** **django.contrib.contenttypes.models** **import** ContentType

content_type = ContentType.objects.get_for_model(BlogPost)

permission = Permission.objects.create(

codename='can_publish',

name='Can Publish Posts',

content_type=content_type,

)

## Authentication in Web requests**[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#authentication-in-web-requests)**

Django uses [sessions](https://docs.djangoproject.com/en/2.0/topics/http/sessions/) and middleware to hook the authentication system into **[request objects](https://docs.djangoproject.com/en/2.0/ref/request-response/#django.http.HttpRequest)**.

These provide a **[request.user](https://docs.djangoproject.com/en/2.0/ref/request-response/#django.http.HttpRequest.user)** attribute on every request which represents the current user. If the current user has not logged in, this attribute will be set to an instance of **[AnonymousUser](https://docs.djangoproject.com/en/2.0/ref/contrib/auth/#django.contrib.auth.models.AnonymousUser)**, otherwise it will be an instance of **[User](https://docs.djangoproject.com/en/2.0/ref/contrib/auth/#django.contrib.auth.models.User)**.

You can tell them apart with **[is_authenticated](https://docs.djangoproject.com/en/2.0/ref/contrib/auth/#django.contrib.auth.models.User.is_authenticated)**, like so:

**if** request.user.is_authenticated:

*# Do something for authenticated users.*

...

**else**:

*# Do something for anonymous users.*

### **How to log a user in[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#how-to-log-a-user-in)**

If you have an authenticated user you want to attach to the current session - this is done with a **[login()](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.login)** function.

`login`(*request*, *user*, *backend=None*)[[source]](https://docs.djangoproject.com/en/2.0/_modules/django/contrib/auth/#login)[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.login)

To log a user in, from a view, use [login()](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.login). It takes an [HttpRequest](https://docs.djangoproject.com/en/2.0/ref/request-response/#django.http.HttpRequest) object and a [User](https://docs.djangoproject.com/en/2.0/ref/contrib/auth/#django.contrib.auth.models.User) object. [login()](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.login) saves the user’s ID in the session, using Django’s session framework.

Note that any data set during the anonymous session is retained in the session after a user logs in.

This example shows how you might use both **[authenticate()](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.authenticate)** and **[login()](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.login)**:

**from** **django.contrib.auth** **import** authenticate, login

**def** my_view(request):

username = request.POST['username']

password = request.POST['password']

user = authenticate(request, username=username, password=password)

**if** user **is** **not** **None**:

login(request, user)

*# Redirect to a success page.*

...

**else**:

*# Return an 'invalid login' error message.*

### **How to log a user out[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#how-to-log-a-user-out)**

**`logout`(*request*)[[source]](https://docs.djangoproject.com/en/2.0/_modules/django/contrib/auth/#logout)[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.logout)**

To log out a user who has been logged in via **[django.contrib.auth.login()](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.login)**, use **[django.contrib.auth.logout()](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.logout)**within your view. It takes an **[HttpRequest](https://docs.djangoproject.com/en/2.0/ref/request-response/#django.http.HttpRequest)** object and has no return value. Example:

**from** **django.contrib.auth** **import** logout

**def** logout_view(request):

logout(request)

*# Redirect to a success page.*

### **The login_required decorator[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#the-login-required-decorator)**

**`login_required`(*redirect_field_name='next'*, *login_url=None*)[[source]](https://docs.djangoproject.com/en/2.0/_modules/django/contrib/auth/decorators/#login_required)[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.decorators.login_required)**

As a shortcut, you can use the convenient **[login_required()](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.decorators.login_required)** decorator:

**from** **django.contrib.auth.decorators** **import** login_required

@login_required

**def** my_view(request):

...

**[login_required()](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.decorators.login_required)** does the following:

- If the user isn’t logged in, redirect to **[settings.LOGIN_URL](https://docs.djangoproject.com/en/2.0/ref/settings/#std:setting-LOGIN_URL)**, passing the current absolute path in the query string. Example: **/accounts/login/?next=/polls/3/**.
- If the user is logged in, execute the view normally. The view code is free to assume the user is logged in.

By default, the path that the user should be redirected to upon successful authentication is stored in a query string parameter called **"next"**. If you would prefer to use a different name for this parameter, **[login_required()](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.decorators.login_required)** takes an optional **redirect_field_name** parameter:

**from** **django.contrib.auth.decorators** **import** login_required

@login_required(redirect_field_name='my_redirect_field')

**def** my_view(request):

…

### **The LoginRequired mixin[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#the-loginrequired-mixin)**

When using [class-based views](https://docs.djangoproject.com/en/2.0/topics/class-based-views/), you can achieve the same behavior as with **login_required** by using the**LoginRequiredMixin**. This mixin should be at the leftmost position in the inheritance list.

***class* `LoginRequiredMixin`[¶](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.mixins.LoginRequiredMixin)**

If a view is using this mixin, all requests by non-authenticated users will be redirected to the login page or shown an HTTP 403 Forbidden error, depending on the **[raise_exception](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.mixins.AccessMixin.raise_exception)** parameter.

You can set any of the parameters of **[AccessMixin](https://docs.djangoproject.com/en/2.0/topics/auth/default/#django.contrib.auth.mixins.AccessMixin)** to customize the handling of unauthorized users:

**from** **django.contrib.auth.mixins** **import** LoginRequiredMixin

**class** **MyView**(LoginRequiredMixin, View):

login_url = '/login/'

redirect_field_name = 'redirect_to'