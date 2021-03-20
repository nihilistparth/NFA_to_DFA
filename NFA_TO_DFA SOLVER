#include <bits/stdc++.h>
#include <iostream>
#include <chrono>
using namespace std::chrono;
using namespace std;
#define int1 int
#define int unsigned long long int

#define db(...) __f(#__VA_ARGS__, __VA_ARGS__)

template <typename Arg1>
void __f(const char *name, Arg1 &&arg1)
{
	cout << name << " : " << arg1 << '\n';
}
template <typename Arg1, typename... Args>
void __f(const char *names, Arg1 &&arg1, Args &&...args)
{
	const char *comma = strchr(names + 1, ',');
	cout.write(names, comma - names) << " : " << arg1 << " | ";
	__f(comma + 1, args...);
}
struct NFA
{
	int n, m;	//size of 2D matrix and m also repreents the Input alphabet set
	int **arr;	//2D matrix to store tansition map
	int ss[32]; //start states
	int ss_size;
	int fs_size;
	int SSB = 0; //start state binary representation
	int FSB = 0; //final state binary representation
	int fs[32];	 //final states
	NFA(int x, int y)
	{
		n = x;
		m = y;
		arr = (int **)malloc(n * sizeof(int *));
		for (int i = 0; i < n; i++)
			arr[i] = (int *)malloc(m * sizeof(int));
		for (int i = 0; i < n; i++)
		{
			for (int j = 0; j < m; j++)
			{
				arr[i][j] = 0;
			}
		}
	}
	void insert1(int p, int a, int q)
	{
		int k = arr[p][q];
		//db(k);
		arr[p][a] |= (1 << q);
		//db(arr[p][a]);
	}
	void insert_ss(int a[])
	{ //insert start states
		// for (int i = 0; i < 32; i++) {
		// 	cout << a[i] << " ";
		// }
		// cout << endl;
		memset(ss, -1, sizeof(ss));
		for (int i = 0; i < 32; i++)
		{
			//db(a[i]);
			ss[i] = a[i];
			SSB |= (1 << a[i]);

			//cout << ss[i] << " ";
		}
		ss_size = 0;
		for (int i = 0; i < 32; i++)
		{
			if (ss[i] != -1)
			{
				//db(i, ss[i]);
				ss_size++;
			}
		}
		//cout << endl;
	}
	void insert_fs(int a[])
	{ //insert final states
		for (int i = 0; i < 32; i++)
		{
			fs[i] = a[i];
			if (a[i] != -1)
				FSB |= (1 << a[i]);

			//db(a[i]);
		}
		fs_size = 0;
		for (int i = 0; i < 32; i++)
		{
			if (fs[i] != -1)
			{
				fs_size++;
			}
		}
	}
	void show()
	{ //used to debug and print NFA transition map if neccessary
		for (int i = 0; i < n; i++)
		{
			for (int j = 0; j < m; j++)
			{
				cout << arr[i][j] << " ";
			}
			cout << endl;
		}
	}
	void print()
	{
		cout << "Input NFA" << endl;
		cout << "Number of states: " << n << endl;
		cout << "Input alphabet: {";
		for (int i = 0; i < m; i++)
		{
			cout << i;
			if (i != m - 1)
			{
				cout << ", ";
			}
		}
		cout << "}" << endl;
		cout << "Start states: {";
		int k1 = 0;
		//db(ss_size);
		for (int i = 0; i < 32; i++)
		{
			if (ss[i] != -1)
			{
				cout << ss[i];
				if (i != 31 and k1 < ss_size - 1)
				{
					cout << ", ";
					k1++;
				}
			}
		}
		cout << "}" << endl;
		k1 = 0;
		cout << "Final states: {";
		for (int i = 0; i < 32; i++)
		{
			if (fs[i] != -1)
			{
				cout << fs[i];
				if (i < 31 and k1 < fs_size - 1)
				{
					cout << ", ";
					k1++;
				}
			}
		}
		cout << "}" << endl;
		cout << "Transition function" << endl;
		for (int i = 0; i < n; i++)
		{
			for (int j = 0; j < m; j++)
			{
				cout << "Delta (" << i << ", " << j << ") = {";
				int z = arr[i][j];
				int cnt1 = 0;
				for (int k = 0; k < 32; k++)
				{
					int k2 = (1 << k);
					if (k2 & z)
					{
						cnt1++;
						//cout << k << ", ";
					}
				}
				for (int k = 0; k < 32; k++)
				{
					int k2 = (1 << k);
					if (k2 & z)
					{
						cout << k;
						//l++;

						if (cnt1 > 1)
						{
							cnt1--;
							cout << ", ";
						}
					}
				}
				cout << "}" << endl;
				//cout << "}" << endl;
			}
			//cout << endl;
		}
	}
};
struct DFA
{
	int n, m;	//size of 2D matrix and m also repreents the Input alphabet set
	int **arr;	//2D matrix to store tansition map
	int ss = 0; //start state
	int fs_size = 0;
	int *fs = new int[10000000]; //final states
	DFA(int x, int y)
	{
		n = x;
		m = y;
		arr = (int **)malloc(n * sizeof(int *));
		for (int i = 0; i < n; i++)
			arr[i] = (int *)malloc(m * sizeof(int));
		for (int i = 0; i < n; i++)
		{
			for (int j = 0; j < m; j++)
			{
				arr[i][j] = 0;
			}
		}
	}
	void show()
	{
		cout << "Number of states: " << n << endl;
		cout << "Input alphabet: { ";
		for (int i = 0; i < m; i++)
		{
			cout << i;
			if (i != m - 1)
			{
				cout << ", ";
			}
		}
		cout << "}" << endl;
		cout << "start state of DFA is = " << ss << endl;

		int ans = 0;
		if (fs_size < 100)
		{
			//cout << "Final states of DFA are = {";
			for (int i = 0; i < fs_size; i++)
			{
				for (int j = 0; j < 32; j++)
				{
					if (fs[i] & (1 << j))
					{
						//cout << j + (i * 32) << ", ";
						ans++;
					}
				}
			}
			//cout << "}" << endl;
		}
		int f_size = 0;
		if (fs_size < 100)
		{
			// cout << "Final states of DFA are = {";
			for (int i = 0; i < fs_size; i++)
			{
				for (int j = 0; j < 32; j++)
				{
					if (fs[i] & (1 << j))
					{
						// cout << j + (i * 32) << ", ";
						f_size++;
						//ans++;
					}
				}
			}
			// cout << "}" << endl;
		}
		if (fs_size > 1000000)
		{
			cout << "Number of Final states of DFA are " << fs_size << endl;
		}

		else
			cout << "Number of Final states of DFA are " << f_size << endl;
		if (fs_size < 100)
		{
			cout << "Final states of DFA are = {";
			for (int i = 0; i < fs_size; i++)
			{
				for (int j = 0; j < 32; j++)
				{
					if (fs[i] & (1 << j))
					{
						cout << j + (i * 32) << ", ";
						//ans++;
					}
				}
			}
			cout << "}" << endl;
		}
		cout << "Transition function" << endl;
		if (n > 64)
		{
			cout << "too big array" << endl;
		}
		else
		{
			cout << "   ";
			for (int i = 0; i < n; i++)
			{
				unsigned k = i;
				printf("%0.2u ", k);
			}
			cout << endl;
			for (int i = 0; i < 3 * n + 2; i++)
			{
				cout << "-";
			}
			cout << endl;
			for (int j = 0; j < m; j++)
			{
				cout << j << " |";
				for (int i = 0; i < n; i++)
				{
					//cout << arr[i][j] << "   ";
					unsigned k = arr[i][j];
					printf("%0.2u ", k);
				}
				cout << endl;
			}
		}
		//cout << "+++ Reachable states:"
	}
};
void printNFA(NFA N)
{
	N.print();
}
void readNFA(NFA *N, string nfas)
{
	// ifstream iFile("input.txt");
	ifstream iFile(nfas);
	int n, m;
	iFile >> n;
	iFile >> m;
	int a[32];
	int b[32];
	memset(a, -1, sizeof(a));
	memset(b, -1, sizeof(b));
	int i = 0;
	while (true)
	{
		int x;
		iFile >> x;
		a[i] = x;
		i++;
		if (x == -1)
			break;
	}
	i = 0;
	while (true)
	{
		int x;
		iFile >> x;
		b[i] = x;
		i++;
		if (x == -1)
			break;
	}
	while (true)
	{
		int x, y, z;
		iFile >> x;

		if (iFile.eof() or x == -1)
			break;
		iFile >> y >> z;
		N->insert1(x, y, z);
	}

	N->insert_fs(b);
	N->insert_ss(a);
}

DFA *subsetcons(NFA *N)
{
	int n = pow(2, N->n);
	int m = N->m;
	//DFA D1(n, m);
	DFA *D1 = new DFA(n, m);
	//D3  =
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < m; j++)
		{
			for (int k = 0; k < N->n; k++)
			{
				if (i & (1 << k))
				{
					D1->arr[i][j] |= N->arr[k][j];
				}
			}
		}
	}
	return D1;
}
void Finalstates(DFA *D, NFA *N)
{
	//db(N->FSB);
	for (int i = 0; i < pow(2, N->n); i++)
	{
		if ((N->FSB) & (i))
		{
			//db(i, N->FSB);
			int cur = i % 32;
			int block = i / 32;
			int power = (1 << cur);
			if (((D->fs[block]) & power) == 0)
			{
				(D->fs_size)++;
				//db(D->fs_size);
				D->fs[block] |= power;
			}
		}
	}
	//db((D->fs_size));
}
void startstates(DFA *D, NFA *N)
{
	for (int i = 0; i < N->ss_size; i++)
	{
		if (N->ss[i] != -1)
			D->ss |= (1 << N->ss[i]);
		else
		{
			break;
		}
	}
}
void dfs(int cur, DFA *D, int *vis)
{
	vis[cur] = 1;
	for (int i = 0; i < D->m; i++)
	{
		if (!vis[D->arr[cur][i]])
		{
			dfs(D->arr[cur][i], D, vis);
		}
	}
}
int *res2 = new int[500000000];
int sz = 0;
int *findreachable(DFA *D)
{
	int *vis = new int[D->n + 10000];
	memset(vis, 0, sizeof(vis));
	dfs(D->ss, D, vis);
	long long ans = 0;

	for (int i = 0; i < D->n; i++)
	{
		if (vis[i])
		{
			ans++;
		}
	}
	//cout << ans << endl;
	int *res = new int[D->n + 10000];
	int j = 0;
	memset(res, -1, sizeof(res));
	for (int i = 0; i < D->n; i++)
	{
		if (vis[i])
		{
			res[j] = i;
			res2[j] = res[j];
			j++;
		}
	}
	//db(ans);
	sz = ans;
	return res;
}
DFA *rmunreachable(DFA *D, int *res)
{
	int m1 = D->m;
	//int n1 = sizeof(res) / sizeof(res[0]);
	//db(n1);
	DFA *D1 = new DFA(sz, m1);
	int cur = 0;
	int *mp = new int[100000000];
	memset(mp, -1, sizeof(mp));
	for (int i = 0; i < sz; i++)
	{
		int idx = res[i];
		mp[idx] = i;
	}
	for (int i = 0; i < sz; i++)
	{
		for (int j = 0; j < m1; j++)
		{
			int idx = res2[i];
			if (idx == D->ss)
			{
				D1->ss = i;
			}
			int x = D->arr[idx][j];
			D1->arr[i][j] = mp[x];
			int block = idx / 32;
			int cur = idx % 32;
			int power = (1 << cur);
			if (((D->fs[block]) & power) != 0)
			{
				(D1->fs_size)++;
				int p = i % 32;
				int p2 = (1 << p);
				D1->fs[i / 32] |= p2;
			}
		}
	}
	return D1;
}

void findequiv(DFA *D1, int **M)
{

	int n1 = D1->n;
	int f[n1];
	int k = 0;
	for (int i = 0; i < D1->fs_size; i++)
	{
		for (int j = 0; j < 32; j++)
		{
			if (D1->fs[i] & (1 << j))
			{
				f[k] = j + (i * 32);
				//ans++;
				k++;
			}
		}
	}
	//db(k) ;
	//db
	for (int j = 0; j < D1->n; j++)
	{
		int chk = 0;
		for (int i = 0; i < k; i++)
		{
			if (f[i] == j)
			{
				chk = 1;
			}
		}
		if (chk == 0)
		{
			for (int i = 0; i < k; i++)
			{
				M[f[i]][j] = 1;
				M[j][f[i]] = 1;
			}
		}
	}

	int chk = 1;
	int t = 2, l1 = 0;
	while (chk)
	{
		l1++;
		chk = 0;
		for (int i = 0; i < D1->n; i++)
		{
			for (int j = 0; j < D1->n; j++)
			{

				if (M[i][j] == 1 || M[j][i] == 1)
					continue;

				for (int z = 0; z < D1->m; z++)
				{
					int x = D1->arr[i][z];
					int y = D1->arr[j][z];
					// //db(M[x][y], x, y) ;
					if (M[x][y] == 1 || M[y][x] == 1)
					{
						M[i][j] = 1;
						M[j][i] = 1;
						chk = 1;
						// //db(M[i][j], i, j) ;
					}
				}

				// if (!chk) {
				// 	break;
				// }
			}
		}
	}
	// //db(l1) ;
	int *mp = new int[100000];
	memset(mp, 0, sizeof(mp));
	int c = 0;
	int l = 0;
	//int t = 0;
	for (int i = 0; i < D1->n; i++)
	{
		if (!mp[i])
		{
			c++;
			l = i;
		}
		mp[i] = 1;
		for (int j = i; j < D1->n; j++)
		{
			if (M[i][j] == 0)
			{
				if (!mp[j])
				{
					c++;
					mp[j];
					l = i;
				}
			}
		}
	}
	int mp1[n1];
	for (int i = 0; i < n1; i++)
		mp1[i] = 0;

	int j = 0;

	for (int i = 0; i < n1; i++)
	{

		int flag = 0;

		if (mp1[i] != 1)
		{
			flag = 1;
			cout << "Group " << j << " = {";
			for (int k = i; k < n1; k++)
			{
				if (M[i][k] == 0)
				{
					cout << k << ", ";
					mp1[k] = 1;
				}
			}
			j++;
			cout << "}" << endl;
		}
	}
}

DFA *collapse(DFA *D, int **M)
{

	int n1 = D->n, size_ = 0, chk = 1;
	int *mp = new int[n1 + 5];
	for (int i = 0; i < n1; i++)
		mp[i] = 0;

	int g = -1;
	int *grp_name = new int[n1], j = 0;
	memset(grp_name, -1, sizeof(grp_name));
	int stidx = -1;
	int mp1[D->n + 100];
	int k = 0;
	for (int i = 0; i < D->n; i++)
	{

		if (mp[i] == 1)
			continue;

		mp[i] = 1;
		size_++;
		grp_name[i] = i;
		mp1[k++] = i;
		if (i == D->ss)
		{
			stidx = i;
		}
		//db(stidx);
		for (int j = i; j < D->n; j++)
		{
			// db(M[i][j], i, j, size_) ;
			if (!M[i][j])
			{
				if (mp[j] == 0)
				{
					if (j == D->ss)
					{
						stidx = i;
					}
					mp[j] = 1;
					grp_name[j] = i;

					// size_++;
				}
			}
		}
	}

	

	DFA *D1 = new DFA(size_, D->m);
	int mp2[D->n + 100];
	for (int i = 0; i < k; i++)
	{
		int id = mp1[i];
		mp2[id] = i;
	}
	
	for (int i = 0; i < size_; i++)
	{
		for (int j = 0; j < D1->m; j++)
		{
			int nxt = D->arr[mp1[i]][j];
			int nxt_grp = grp_name[nxt];
			int nex = mp2[nxt_grp];
			D1->arr[i][j] = nex;
			if (mp1[i] == stidx)
			{
				D1->ss = i;
				
			}
			int block = mp1[i] / 32; 

			int cur = mp1[i] % 32;
			int power = (1 << cur);
			if (((D->fs[block]) & power) != 0)
			{
				(D1->fs_size)++;
				int p = i % 32;
				int p2 = (1 << p);
				D1->fs[i / 32] |= p2;
			}
		}
		
	}

	return D1;
}

int32_t main()
{
	string nfas = "input.txt";
	cout << "Enter Input file name" << endl;
	cin >> nfas;
	ifstream iFile(nfas);

	// ifstream iFile("input.txt");

	int n, m;
	iFile >> n;
	iFile >> m;
	NFA N(n, m);
	readNFA(&N, nfas);
	printNFA(N);
	DFA *D = subsetcons(&N);
	Finalstates(D, &N);
	startstates(D, &N);
	cout << "+++ Converted DFA" << endl;
	D->show();
	int *res = new int[D->n + 1000];
	memset(res, -1, sizeof(res));
	res = findreachable(D);
	cout << "+++ Reachable states: { ";
	int re_size = 0;
	for (int i = 0; i < D->n + 1000; i++)
	{
		if (res[i] != -1 and res[i] > 0)
		{
			if (i > 0)
			{
				cout << ", ";
			}
			cout << res[i];
			re_size++;
		}
	}
	cout << "}" << endl;
	//db(re_size) ;
	int **M;
	M = (int **)malloc(sz * sizeof(int *));
	for (int i = 0; i < sz; i++)
		M[i] = (int *)malloc(sz * sizeof(int));
	for (int i = 0; i < sz; i++)
	{
		for (int j = 0; j < sz; j++)
		{
			M[i][j] = 0;
		}
	}

	DFA *D1 = rmunreachable(D, res);

	cout << "+++ Reduced DFA after removing unreachable states" << endl;
	D1->show();
	cout << "+++ Equivalent states" << endl;
	findequiv(D1, M);

	if (M == NULL)
		cout << "NULL" << endl;

	DFA *D2 = collapse(D1, M);
	cout << "+++ Reduced DFA after collapsing equivalent states" << endl;
	D2->show();
	return 0;
}
