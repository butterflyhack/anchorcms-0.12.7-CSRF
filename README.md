# anchorcms-0.12.7-CSRF
CSRF (Cross-site request forgery) Vulnerability discovered in Anchor CMS v0.12.7 and that can delete posts.

# Vulnerability Analysis  

Request interface for adding, deleting, modifying and checking posts in anchor/routes/posts.php.

let us see code it delete a posts. 
```
    /**
     * Delete post
     */
    Route::get('admin/posts/delete/(:num)', function ($id) {
        Post::find($id)->delete();
        Comment::where('post', '=', $id)->delete();

        Query::table(Base::table('post_meta'))
             ->where('post', '=', $id)
             ->delete();

        Notify::success(__('posts.deleted'));

        return Response::redirect('admin/posts');
    });
```
There is no check on token or referer and delete directly.

# PoC

1. Login in as a admin.
2. 
# 


