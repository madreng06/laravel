# laravel
     <form method="post" action="{{route('order') }}">
            @csrf
            <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label">Название товара</label>
                <input type="text" name="name_order" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
                
            </div>
            <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Цена товара</label>
                <input type="text" class="form-control" id="exampleInputPassword1" name="price_order">
            </div>
             <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Адресс заказа</label>
                <input type="text" class="form-control" id="exampleInputPassword1" name="address_order">
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
        </form>
<div class="card-body">
        <div class="row row-cols-1 row-cols-md-3 g-4">
            <div class="col">
            <@foreach ($orders as $order)>
                <div class="card">
                <img src="..." class="card-img-top" alt="...">
                <div class="card-body">
                    <h5 class="card-title">#{{ $order -> id }}</h5>
                    <p class="card-text">{{ $order -> name_order }}</p>
                    <p class="card-text">{{ $order -> price_order }}</p>
                    <p class="card-text">{{ $order -> address_order }}</p>
                </div>
                </div>
            </div>
             @endforeach
        </div>
        </div>
        ############
        web
        public function createOrder(Request $request){
        DB::table('orders')
            ->insert([
                'user_id' => Auth::id(),
                'name_order' => $request -> name_order,
                'price_order' => $request -> price_order,
                'address_order' => $request -> address_order,
            ]);
        return redirect(route('home')) -> with(['msg' => 'Заказ добавлен']);
    }
    ####################
    home
     public function index()
    {
        $orders = DB::table('orders')
            ->where('user_id', Auth::id())
            ->get();
        return view('home',['orders' => $orders]);
    }
