views.py 
==========

-------------------
What is views.py?
-------------------

views.py answers this question:
    “When a URL is requested, what should Django do and what should it return?”

A view:
	- Receives a **request**
	- Runs **Python logic**
	- Returns a **response**

======================================================================================================================================

**Django Flow**

.. code-block:: bash 
    
    Browser
      ↓
    urls.py
      ↓
    views.py
      ↓
    Response (HTML / JSON / Text)

======================================================================================================================================

--------------------------
Types of Views in Django
--------------------------

There are two main types:
	1.	**Function-Based Views (FBV)**  beginner-friendly
	2.	**Class-Based Views (CBV)**  scalable & reusable

We’ll start with **Function-Based Views.**

======================================================================================================================================

1) Function-Based Views (FBV)
-------------------------------

**What an FBV is**

An FBV is simply a Python function that:
	#.	receives a request object
	#.	does some logic
	#.	returns a HttpResponse (or JsonResponse, or render())

FBV shape (always the same)

.. code-block:: python 

    def my_view(request, ...):
        # 1) read request data (GET/POST/headers/user)
        # 2) do logic (DB query, validation, etc.)
        # 3) return response

======================================================================================================================================

**A) Basic FBV examples**

**Return plain text**

.. code-block:: python 

    from django.http import HttpResponse

    def home(request):
        return HttpResponse("Hello from FBV")

**Return HTML template**

.. code-block:: python 

    from django.shortcuts import render

    def home(request):
        return render(request, "myapp/home.html")

**Return JSON (API style)**    

.. code-block:: python 

    from django.http import JsonResponse

    def status(request):
        return JsonResponse({"ok": True, "message": "Server is running"})

======================================================================================================================================

**B) Reading request data in FBV**

**Query string: ?q=phone**

.. code-block:: python 

    def search(request):
        q = request.GET.get("q", "")   # GET parameters
        return HttpResponse(f"You searched: {q}")

Form POST data

.. code-block:: python 

    def submit(request):
        if request.method == "POST":
            name = request.POST.get("name")
            return HttpResponse(f"Received: {name}")
        return HttpResponse("Send a POST request")

======================================================================================================================================

**C) CRUD example with FBV**

Suppose you have a model Post.

.. code-block:: python 

    from django.shortcuts import render, redirect, get_object_or_404
    from .models import Post

    def post_list(request):
        posts = Post.objects.all()
        return render(request, "myapp/post_list.html", {"posts": posts})

    def post_detail(request, pk):
        post = get_object_or_404(Post, pk=pk)
        return render(request, "myapp/post_detail.html", {"post": post})

    def post_create(request):
        if request.method == "POST":
            title = request.POST.get("title")
            Post.objects.create(title=title)
            return redirect("post_list")
        return render(request, "myapp/post_form.html")

✅ Easy to read.

❌ Repetition grows when you build many CRUD pages.

======================================================================================================================================

**D) Pros / Cons of FBV**

✅ Pros
	- Very easy to learn and debug
	- Straight-line logic, clear flow
	- Great for small pages and custom logic

❌ Cons
	- Repetition for common CRUD patterns
	- Harder to reuse behavior across many views
	- You manually handle GET/POST patterns again and again

======================================================================================================================================

2) Class-Based Views (CBV) — scalable & reusable
---------------------------------------------------

**What a CBV is**

A **CBV** is a Python class where each HTTP method is a method:
	- get() handles GET
	- post() handles POST
	- put(), delete() etc.

You connect it in urls.py using .as_view().

======================================================================================================================================

**A) Basic CBV example**

.. code-block:: python 

    from django.views import View
    from django.http import HttpResponse

    class HomeView(View):
        def get(self, request):
            return HttpResponse("Hello from CBV")

**urls.py**

.. code-block:: python 

    from django.urls import path
    from .views import HomeView

    urlpatterns = [
        path("", HomeView.as_view(), name="home"),
    ]

as_view() converts the class into a callable view function Django can run.

======================================================================================================================================

**B) Why CBV feels “powerful”**

Because CBVs can be built using:
	- **inheritance**
	- **mixins**
	- **generic views** (ListView, DetailView, CreateView…)

This reduces code and repetition massively.

======================================================================================================================================

**The most important CBVs: Generic Views**

**1) ListView (list objects)**

.. code-block:: python 

    from django.views.generic import ListView
    from .models import Post

    class PostListView(ListView):
        model = Post
        template_name = "myapp/post_list.html"
        context_object_name = "posts"

That’s it. Django does the query + context + render.

======================================================================================================================================

**2) DetailView (one object)**

.. code-block:: python 

    from django.views.generic import DetailView
    from .models import Post

    class PostDetailView(DetailView):
        model = Post
        template_name = "myapp/post_detail.html"
        context_object_name = "post"

**3) CreateView (create object)**

.. code-block:: python 

    from django.views.generic import CreateView
    from django.urls import reverse_lazy
    from .models import Post

    class PostCreateView(CreateView):
        model = Post
        fields = ["title", "body"]
        template_name = "myapp/post_form.html"
        success_url = reverse_lazy("post_list")

**4) UpdateView / DeleteView**

They work the same way. Very clean.

======================================================================================================================================

**C) Handling logic in CBV (override methods)**

**Example: filter posts by query param**

.. code-block:: python 

    class PostListView(ListView):
        model = Post
        template_name = "myapp/post_list.html"

        def get_queryset(self):
            qs = super().get_queryset()
            q = self.request.GET.get("q")
            if q:
                qs = qs.filter(title__icontains=q)
            return qs

======================================================================================================================================

**D) Mixins (reusable behavior)**

Mixins are “plugins” you add to CBVs.

Example: login required

.. code-block:: python 

    from django.contrib.auth.mixins import LoginRequiredMixin
    from django.views.generic import ListView

    class PrivatePostListView(LoginRequiredMixin, ListView):
        model = Post

Now only logged-in users can access.

======================================================================================================================================

**E) Pros / Cons of CBV**

✅ Pros
	- Less repetition, especially for CRUD
	- Clean, scalable for big apps
	- Mixins allow reusable features (auth, permissions, etc.)
	- Generic views save lots of code

❌ Cons
	- Harder at the beginning
	- Inheritance chain can confuse (where did this behavior come from?)
	- Debugging sometimes needs deeper understanding

======================================================================================================================================

**FBV vs CBV**

.. list-table:: 
    :header-rows: 1

    * - Feature
      - FBV
    * - CBV
      - Learning
    * - ✅ easiest
      - ⚠️ medium
    * - CRUD speed
      - ❌ more code
    * - ✅ very fast
      - Reuse
    * - ❌ manual
      - ✅ mixins/inheritance
    * - Clarity
      - ✅ direct
    * - ⚠️ sometimes hidden
      - Best for
    * - small/custom logic
      - big scalable apps

======================================================================================================================================

-----------------------
When to choose what?
-----------------------

Choose FBV when:
	- You’re learning
	- The view is simple and custom
	- You need full control without “magic”

Choose CBV when:
	- You have many pages with similar patterns (CRUD)
	- You want scalable organization
	- You need mixins (auth/permissions) a lot


